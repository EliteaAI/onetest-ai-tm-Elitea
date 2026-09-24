---
id: ELITEA-3408
title: "Pre-Existing User Token Named elitea-system Is Renamed to elitea-system-conflict-<id> by Migration"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, migration]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3408: Conflicting Pre-Existing Token Renamed on Migration

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm that if a user already has their own personal token literally named `elitea-system` (created before this feature existed, coincidentally or intentionally), the DB migration deterministically renames it to `elitea-system-conflict-<id>` at boot, unconditionally — clearing the way for the real system token to be created under the reserved name without violating the new unique index. Also confirm the same eviction logic applies when `ensure_system_token()` encounters a name-matching-but-expiring row.

**Coverage:** Design detail from `auth_core`#12 — alembic migration `202609161200`, conflict-rename pattern; rollback plan notes these renamed rows are never restored

## Preconditions

- A user with a pre-existing personal token named exactly `elitea-system` that has a non-null `expires` value (i.e., it is NOT already a valid system token by the `name == "elitea-system" AND expires IS NULL` definition)
- Note this token's id in advance

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the pre-existing token's current name is `elitea-system` and it has a non-null expiry. | Confirmed — this is a genuine reserved-name conflict, not a real system token. |
| 2 | Trigger the migration boot path (apply alembic revision `202609161200`, or restart the service in an environment where this hasn't yet run). | Migration runs without error. |
| 3 | Re-query the token by its known id. | Name has changed to `elitea-system-conflict-<id>` (using that token's own id). Its `expires` value and all other fields are otherwise unchanged. |
| 4 | Check the `pylon_auth` boot log for this event. | A log entry records the renamed row's id and owning user id. |
| 5 | Confirm the affected user now also has a real `elitea-system` token (`expires IS NULL`) — either created by this same migration/backfill or by their next login. | User has both: the renamed conflict token (still usable, just under a new name) and a genuine system token. |
| 6 | Attempt to use the renamed `elitea-system-conflict-<id>` token for authentication (e.g. as an API credential) as it was used before. | Still works normally — renaming doesn't revoke or break the token's function, only its name. |

## Expected Final State

The conflicting token survives under a new, non-reserved name and keeps working; the user gains a distinct real system token; no unique-index violation occurs.

## Pass/Fail Criteria

**Pass:**
- Conflicting token is renamed exactly as documented, remains functional, and is logged; a genuine system token subsequently exists for that user

**Fail:**
- Migration fails/errors due to the naming collision (unique index violation not avoided)
- The conflicting token is deleted or broken instead of renamed
- No boot-log record of the rename exists
