---
id: ELITEA-3409
title: "Concurrent System Token Provisioning for the Same User Never Creates Duplicates"
priority: medium
type: integration
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, concurrency]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3409: Concurrent Provisioning Race Is Safely Resolved by the Unique Index

**Module:** Tokens · **Priority:** Medium · **Type:** Integration

**Objective:** Confirm that if two concurrent code paths attempt to provision a system token for the same user at the same moment (e.g. a login self-heal racing a backfill migration run, or two rapid parallel logins), the partial unique index `uq_auth_core__token_system_per_user` guarantees only one row is ever created — the loser of the race is handled gracefully (counted, not raised as an unhandled error to the caller).

**Coverage:** Design detail from `auth_core`#12 — partial unique index on `(user_id) WHERE name = 'elitea-system'`, `NOT EXISTS`-guarded insert

## Preconditions

- A user with no existing system token
- Ability to trigger two near-simultaneous calls to `ensure_system_token(user_id)` for the same user (e.g. two parallel requests, or a login self-heal fired at the same instant as a backfill run covering the same user)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the test user has no `elitea-system` token. | Confirmed absent. |
| 2 | Fire two concurrent `ensure_system_token(user_id)` calls for the same user (e.g. via two parallel login attempts, or one login self-heal overlapping a backfill run touching this user). | Both calls complete without an unhandled exception/500 propagating to either caller. |
| 3 | Query the user's tokens with `include_system=True` immediately after. | Exactly one `elitea-system` token exists — not zero, not two. |
| 4 | If either code path exposes a race-loss counter (e.g. backfill's `reserved_name_conflicts`/internal race counter), inspect it. | The lost race is accounted for internally rather than surfacing as a caller-visible error. |

## Expected Final State

Regardless of timing, exactly one system token exists per user; racing provisioning attempts never produce a duplicate or an unhandled DB constraint error visible to the caller.

## Pass/Fail Criteria

**Pass:**
- Exactly one system token exists after the race; neither caller sees an unhandled exception

**Fail:**
- Two system tokens exist for the same user (index not enforced/violated)
- One of the racing calls surfaces a raw DB constraint-violation error to its caller instead of handling it gracefully
