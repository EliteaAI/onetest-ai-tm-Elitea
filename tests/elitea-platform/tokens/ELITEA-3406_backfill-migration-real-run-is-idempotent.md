---
id: ELITEA-3406
title: "Backfill Migration Real Run Provisions Missing Tokens and Is Idempotent on Re-Run"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, migration]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3406: Backfill Migration Real Run Is Idempotent

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm the real (non-dry-run) backfill actually provisions a system token for every eligible user missing one, correctly counts suspended users as skipped, and — critically — running it again afterward is a safe no-op (`created=0`), never creating duplicates.

**Coverage:** AC — backfill provisions tokens for pre-existing users; idempotency guarantee from the unique index + `NOT EXISTS` guard

## Preconditions

- Same mixed DB state as [[ELITEA-3405]]: users with and without a system token, at least one suspended user
- Dry-run report from ELITEA-3405 available for comparison

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run `migrate_user_system_tokens` with no param (real run). | Task completes; internally calls `auth_backfill_system_tokens(dry_run=False)`. |
| 2 | Compare the real run's report to the prior dry run's report (same DB state). | `created` count matches what the dry run predicted; `skipped_suspended` matches the known suspended-user count. |
| 3 | Query the DB directly for all previously-missing users. | Each now has exactly one `elitea-system` token, `expires IS NULL`. |
| 4 | Query the DB for the suspended user(s). | Still no system token created for them — correctly skipped, not errored. |
| 5 | Re-run `migrate_user_system_tokens` with no param a second time (idempotency check). | Report shows `created: 0` — every eligible user already has a token; `already_present` now covers all previously-missing users too. |
| 6 | Re-confirm DB state after the second run. | No duplicate system tokens for any user; row counts unchanged from after step 3. |

## Expected Final State

Every non-suspended user has exactly one system token after the first real run; re-running is a safe, effect-free no-op.

## Pass/Fail Criteria

**Pass:**
- First run creates the predicted number of tokens and correctly skips suspended users; second run creates zero and changes nothing

**Fail:**
- Second run creates duplicate tokens for any user
- Suspended users get a token created despite being suspended
- Real-run counts diverge unexplainably from the dry-run prediction on identical starting state
