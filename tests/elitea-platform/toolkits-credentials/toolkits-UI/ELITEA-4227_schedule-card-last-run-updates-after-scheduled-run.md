---
id: ELITEA-4227
title: "Schedule Card Last Run Updates After a Scheduled Run"
priority: medium
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:indexer, feat:toolkits, eng:frontend, schedule, last-run]
requirements: [EliteaAI/elitea_issues#7083]
---
# ELITEA-4227: Schedule Card Last Run Updates After a Scheduled Run

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when the schedule triggers a reindex, `Last run` on the schedule card updates to the scheduled run's finish time, replacing the earlier manual run's time.

**Coverage:**
- Scheduled runs count toward `Last run` (the gap reported in the issue)
- The latest finished run wins, whether a user or the schedule started it

## Preconditions

- A toolkit with an index that has at least one completed manual run
- The index schedule is enabled and set to fire within the next few minutes

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the index and note the current `Last run` value on the SCHEDULE card. | `Last run` shows the manual run's finish time. |
| 2 | Wait for the scheduled run to trigger and complete. | A new History row appears for the scheduled run. |
| 3 | Reopen the index and observe the SCHEDULE card. | `Last run` now shows the scheduled run's finish time, not the earlier manual run's time. |
| 4 | Compare the `Last run` value with the newest History row. | The values match. |

## Expected Final State

`Last run` reflects the scheduled run's finish time.

## Pass/Fail Criteria

**Pass:**
- `Last run` updates to the scheduled run's finish time

**Fail:**
- `Last run` keeps the earlier manual run's time, or is missing after a scheduled run
