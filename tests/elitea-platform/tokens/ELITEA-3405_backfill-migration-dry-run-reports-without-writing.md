---
id: ELITEA-3405
title: "Backfill Migration Dry-Run Reports Counts Without Writing Any Tokens"
priority: high
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, migration]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3405: Backfill Migration Dry-Run Reports Without Writing

**Module:** Tokens · **Priority:** High · **Type:** Functional

**Objective:** Confirm running the `migrate_user_system_tokens` admin task with the `dry_run` param produces an accurate report of what *would* happen, without creating, modifying, or deleting any actual token rows.

**Coverage:** AC — backfill task for pre-existing users; admin task `migrate_user_system_tokens` (task group `R-2.0.7`)

## Preconditions

- A DB state with a known mix of users: some with an `elitea-system` token already, some with none, at least one suspended user, and (ideally) at least one user with a pre-existing personal token literally named `elitea-system` with a non-null expiry (a reserved-name conflict — see [[ELITEA-3408]])
- Ability to trigger the `migrate_user_system_tokens` admin task with a `param`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Snapshot the current token table state (row count, names) before running anything. | Baseline recorded. |
| 2 | Run `migrate_user_system_tokens` with `param="dry_run"`. | Task completes successfully; internally calls `auth_backfill_system_tokens(dry_run=True)`. |
| 3 | Inspect the task's returned report. | Report contains keys `dry_run: true`, `users_total`, `already_present`, `missing`, `created`, `skipped_suspended`, `reserved_name_conflicts`, with `created` reflecting how many *would* be created (but see step 4). |
| 4 | Re-snapshot the token table after the dry run. | Identical to the step 1 baseline — zero rows inserted, updated, or deleted. |
| 5 | Re-run with `param="DRY_RUN"` (different casing) and with a whitespace-padded variant (e.g. `" dry_run "`). | Both are recognized as dry-run (case-insensitive, whitespace-tolerant per `is_dry_run()`); no writes occur either time. |

## Expected Final State

The token table is byte-for-byte unchanged after any number of dry runs; the report accurately reflects what a real run would do.

## Pass/Fail Criteria

**Pass:**
- Dry run report contains all documented keys with plausible counts; DB state is provably unchanged after the run, regardless of `dry_run` param casing/whitespace

**Fail:**
- Any row is inserted, updated, or deleted during a dry run
- Report is missing expected keys or reports implausible counts (e.g. `created > missing`)
