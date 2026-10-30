---
id: ELITEA-4226
title: "Schedule Card Shows Last Run After a Manual Reindex"
priority: medium
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:indexer, feat:toolkits, eng:frontend, schedule, last-run]
requirements: [EliteaAI/elitea_issues#7083]
---
# ELITEA-4226: Schedule Card Shows Last Run After a Manual Reindex

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after a manually started reindex finishes, the index schedule card shows a `Last run: <date, time>` line whose value matches the finish time of the newest entry in the index History.

**Coverage:**
- `Last run:` line is rendered on the schedule card above `Next run:`
- Date/time format matches the `Next run` format (viewer's local timezone)
- Manually started runs count toward `Last run`

## Preconditions

- A toolkit with an index that has a schedule configured (enabled)
- User has permission to run a reindex

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the toolkit → Indexes → select the index. | Index details open; the SCHEDULE card is visible. |
| 2 | Start a manual reindex and wait until it completes. | Index status shows completed; a new row appears in History. |
| 3 | Observe the SCHEDULE card. | A `Last run: <date, time>` line is shown above `Next run:`, in the same date/time format. |
| 4 | Compare the `Last run` value with the finish time of the newest History row. | The values match (same instant, viewer's local timezone). |

## Expected Final State

The schedule card shows `Last run` equal to the finish time of the manual reindex.

## Pass/Fail Criteria

**Pass:**
- `Last run` is shown and matches the newest finished History row

**Fail:**
- `Last run` is missing, shows an older run, or uses a different format/timezone than `Next run`
