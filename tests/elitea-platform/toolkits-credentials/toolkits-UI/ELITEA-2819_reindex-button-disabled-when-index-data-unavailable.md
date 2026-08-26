---
id: ELITEA-2819
title: "Reindex Button Disabled When index_data Tool Unavailable"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, indexes, reindex, validation]
requirements: [EL-6252, EL-6371]
---
# ELITEA-2819: Reindex Button Disabled When index_data Tool Unavailable

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Reindex button is disabled when the index_data tool is unavailable or disabled for the toolkit.

**Coverage:**
- Reindex button disabled when index_data tool is disabled
- Button not clickable in disabled state
- Tooltip explains why reindex is unavailable
- No failed indexing attempts when button is disabled

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with an existing index
- The toolkit has the index_data tool (can be enabled/disabled)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexing capability and existing index |
| Index | An existing index on the toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open a toolkit with an existing index. | Toolkit details page opens. |
| 2 | Expand the Tools section. | Tools list displayed. |
| 3 | Locate and disable the "index_data" tool (toggle OFF). | index_data tool is disabled. |
| 4 | Save the toolkit configuration. | Changes saved successfully. |
| 5 | Navigate to the existing index (click on index card or name). | Index details page opens. |
| 6 | Navigate to the Activity view for the index. | Activity view displayed. |
| 7 | Observe the "Reindex" button state. | Reindex button is disabled (grayed out, not clickable). |
| 8 | Hover over the disabled Reindex button. | Tooltip appears explaining that index_data tool is required. |
| 9 | Attempt to click the disabled button. | Button does not respond; no action triggered. |
| 10 | Navigate back to toolkit, enable index_data tool, save. | index_data tool re-enabled. |
| 11 | Return to index Activity view. | Activity view displayed. |
| 12 | Observe the Reindex button state. | Reindex button is now enabled. |

## Expected Final State

Reindex button is enabled when index_data tool is available, disabled with tooltip explanation when unavailable.

## Pass/Fail Criteria

**Pass:**
- Reindex button disabled when index_data tool is disabled
- Tooltip explains the requirement
- Button cannot be clicked when disabled
- Button enabled when index_data tool is available

**Fail:**
- Reindex button enabled when index_data is disabled
- No tooltip on disabled button
- Clicking disabled button triggers indexing (and fails)
- Button state doesn't update after enabling index_data
