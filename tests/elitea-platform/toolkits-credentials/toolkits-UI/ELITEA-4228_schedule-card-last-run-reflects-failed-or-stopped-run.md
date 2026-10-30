---
id: ELITEA-4228
title: "Schedule Card Last Run Reflects a Failed or Stopped Run"
priority: low
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:indexer, feat:toolkits, eng:frontend, schedule, last-run]
requirements: [EliteaAI/elitea_issues#7083]
---
# ELITEA-4228: Schedule Card Last Run Reflects a Failed or Stopped Run

**Module:** Toolkits & Indexes · **Priority:** Low · **Type:** Functional

**Objective:** Verify that a run which failed or was stopped counts as the last run, so `Last run` shows its time instead of the older successful run's time.

**Coverage:**
- Failed runs count toward `Last run`
- Stopped (cancelled) runs count toward `Last run`

## Preconditions

- A toolkit with an index that has a schedule configured and at least one completed run

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the index and note the current `Last run` value. | `Last run` shows the completed run's finish time. |
| 2 | Start a reindex and stop it with the Stop button. | Run ends with a stopped status; a new History row appears. |
| 3 | Observe the SCHEDULE card. | `Last run` shows the stopped run's time. |
| 4 | Make a reindex fail (e.g. temporarily use invalid toolkit credentials) and wait for it to end. | Run ends with a failed status; a new History row appears. |
| 5 | Observe the SCHEDULE card. | `Last run` shows the failed run's time. |

## Expected Final State

`Last run` matches the newest finished History row, whatever its result.

## Pass/Fail Criteria

**Pass:**
- `Last run` updates after both a stopped and a failed run

**Fail:**
- `Last run` stays on the older successful run after a stopped or failed run
