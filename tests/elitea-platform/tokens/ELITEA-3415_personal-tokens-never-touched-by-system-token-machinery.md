---
id: ELITEA-3415
title: "User's Own Personal Tokens Are Never Touched by Migration, Self-Heal, or Runtime Fallback"
priority: high
type: regression
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, regression]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3415: Personal Tokens Are Never Mutated by System-Token Machinery

**Module:** Tokens · **Priority:** High · **Type:** Regression

**Objective:** Confirm that across every new mechanism introduced by this feature — the backfill migration, login self-heal, and runtime fallback — a user's own personal (non-`elitea-system`-named) tokens are never created, modified, renamed, or deleted as a side effect. Only the reserved-name conflict case (a token literally named `elitea-system`, see [[ELITEA-3408]]) is ever touched, and that's a rename, not the ordinary case.

**Coverage:** Regression guarantee spanning `auth_core`#12, `auth_init`#2, `elitea_core`#435 — new machinery is additive/read-mostly with respect to personal tokens

## Preconditions

- A user with two or three personal tokens under ordinary, non-reserved names, with a mix of expiries (some future, some non-expiring)
- Full snapshot of these tokens' ids, names, and expiries taken before exercising any of the flows below

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run the backfill migration task (`migrate_user_system_tokens`, real run) covering this user. | This user's personal tokens are byte-for-byte unchanged (ids, names, expiries) after the run; only a new, separate `elitea-system` row is added if missing. |
| 2 | Log this user out and back in (exercising the self-heal path). | Personal tokens unchanged; login succeeds normally. |
| 3 | Trigger both runtime fallback call sites for this user (who has valid personal tokens, so fallback shouldn't even trigger per [[ELITEA-3411]]). | Personal tokens unchanged; system token, if any, also unused since a valid personal token exists. |
| 4 | Re-snapshot all this user's personal tokens after steps 1-3. | Identical to the pre-test snapshot in every field. |

## Expected Final State

Every personal token this user owned before the test still exists, unchanged, after every new mechanism has run against their account.

## Pass/Fail Criteria

**Pass:**
- No personal token's id, name, or expiry differs from the pre-test snapshot after any of the three flows

**Fail:**
- Any personal token is modified, renamed, or removed by the migration, self-heal, or fallback machinery
