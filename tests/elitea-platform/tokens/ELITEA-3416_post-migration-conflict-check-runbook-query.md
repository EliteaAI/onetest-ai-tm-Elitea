---
id: ELITEA-3416
title: "Runbook's Post-Migration Conflict-Check Query Correctly Surfaces Renamed Rows"
priority: low
type: integration
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, migration, runbook]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3416: Runbook Conflict-Check Query Verification

**Module:** Tokens · **Priority:** Low · **Type:** Integration

**Objective:** Confirm the operational runbook shipped with `admin`#45 includes a working query/procedure for operators to check for reserved-name conflicts after running the migration, and that it correctly surfaces every row the migration renamed to `elitea-system-conflict-<id>` (cross-referenced against the `pylon_auth` boot log from [[ELITEA-3408]]).

**Coverage:** Design detail from `admin`#45 — backfill task ships with a runbook, including a post-migration conflict-check

## Preconditions

- The runbook document for `migrate_user_system_tokens` (from `admin`#45)
- At least one conflict-renamed row exists in the DB (per [[ELITEA-3408]])

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate the runbook's documented conflict-check query/procedure. | Runbook clearly documents how to list all `elitea-system-conflict-*` named rows. |
| 2 | Run the documented query against a DB with at least one known conflict-renamed row. | Query returns that row (and any others), matching what was recorded in the `pylon_auth` boot log at migration time. |
| 3 | Cross-check the query's results against the boot log's recorded id+owner pairs from [[ELITEA-3408]] step 4. | Results match exactly — no renamed row is missed by the query, no extra/phantom rows appear. |
| 4 | Confirm the runbook also documents the rollback plan's explicit statement that renamed rows are never automatically restored by a rollback. | Runbook text matches this behavior — operators are correctly warned not to expect automatic reversal. |

## Expected Final State

An operator following the runbook after a real migration run can reliably and completely identify every reserved-name conflict that occurred.

## Pass/Fail Criteria

**Pass:**
- Documented query surfaces exactly the set of renamed rows, matching the boot log; runbook correctly documents rollback's non-restoration of these rows

**Fail:**
- Query misses a known renamed row, or the runbook's documented procedure doesn't work as written
- Runbook is silent or incorrect about renamed rows not being restored by rollback
