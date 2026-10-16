---
id: ELITEA-3984
title: "Formatted Summary in Toolkit Run History"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:indexing-summary, run-history, formatting]
requirements: [EL-6229]
---
# ELITEA-3984: Formatted Summary in Toolkit Run History

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Toolkit Run History displays a user-readable formatted summary for index_data tool executions.

**Coverage:**
- Toolkit Run History shows formatted summary for index_data runs
- Raw technical output replaced with readable format
- Category breakdowns included in output
- Chunk counts not shown in primary output

## Preconditions

- Logged in to {{base_url}}
- A toolkit with at least one completed indexing operation in Run History

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with index_data execution in history |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes. | Toolkits list displays. |
| 2 | Select a toolkit that has indexing history. | Toolkit details page opens. |
| 3 | Click "Run History" button. | Run History page displays. |
| 4 | Locate an entry where index_data tool was executed. | Entry found with index_data tool. |
| 5 | Click on the entry to view details. | Entry details panel opens. |
| 6 | Observe the output section. | Output displays formatted summary. |
| 7 | Verify the output does NOT show only raw JSON parameters. | Raw JSON parameters not primary output. |
| 8 | Verify the output does NOT show only chunk counts. | No standalone chunk count output. |
| 9 | Verify formatted summary shows indexed/skipped/unsupported/failed counts. | Category breakdowns visible with counts and reasons. |

## Expected Final State

Toolkit Run History displays a user-readable formatted summary for indexing operations with category breakdowns.

## Pass/Fail Criteria

**Pass:**
- Formatted summary displayed for index_data runs
- Category breakdowns (indexed, skipped, unsupported, failed) shown
- Counts and reasons included
- Raw JSON/chunk counts not in primary output

**Fail:**
- Only raw JSON parameters displayed
- Only chunk counts shown
- No category breakdowns
- Missing formatted summary
