---
id: ELITEA-4001
title: "Regression - Reindex Button Disabled When index_data Tool Unavailable"
priority: critical
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, smoke, toolkit-sections-redesign, reindex]
requirements: [EL-6252, EL-6371]
---
# ELITEA-4001: Regression - Reindex Button Disabled When index_data Tool Unavailable

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Regression / Smoke

**Objective:** Verify that Reindex button is disabled when index_data tool is unavailable, preventing failed reindex attempts.

**Coverage:**
- Reindex button disabled when index_data tool is disabled
- Tooltip explains the requirement
- Button enabled when index_data tool is available
- No failed indexing attempts from disabled button

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with an existing index and index_data tool

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexing capability |
| Index | An existing completed index |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open a toolkit with an index. | Toolkit details page opens. |
| 2 | Expand Tools section → disable "index_data" tool. | Tool disabled. |
| 3 | Save the toolkit. | Changes saved. |
| 4 | Navigate to the index → Activity view. | Activity view opens. |
| 5 | Observe Reindex button state. | Button is disabled (grayed out). |
| 6 | Hover over disabled button. | Tooltip explains index_data tool required. |
| 7 | Try clicking the disabled button. | No action triggered. |
| 8 | Navigate back to toolkit → enable index_data tool → save. | Tool enabled and saved. |
| 9 | Return to index Activity view. | Activity view opens. |
| 10 | Observe Reindex button state. | Button is now enabled. |

## Expected Final State

Reindex button correctly reflects index_data tool availability with appropriate disabled state and tooltip.

## Pass/Fail Criteria

**Pass:**
- Button disabled when index_data is disabled
- Tooltip explains the requirement
- Button not clickable when disabled
- Button enabled when index_data is available

**Fail:**
- Button enabled when index_data is disabled
- No tooltip on disabled button
- Button triggers failed indexing
- Button state doesn't update
