---
id: ELITEA-2786
title: "Index Status Indicators on Cards"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, indexes, status]
requirements: []
---
# ELITEA-2786: Index Status Indicators on Cards

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify index cards show correct status indicators for different index states.

**Coverage:**
- In-progress index shows spinner/processing indicator
- Completed index shows "Index is ready!" green status
- Failed/error index shows error indicator
- Status updates reflect real-time changes

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with indexing capability
- PgVector and Embedding Model configured

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any indexing-capable toolkit |
| Data Source | Small data source for quick indexing |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select a toolkit → Indexes panel. | Indexes panel displayed. |
| 2 | Click "+ Index" and start creating a new index with valid data. | App navigates to the new index's details page with the "Activity" tab selected by default; blue in-progress status shown. |
| 3 | Navigate to the toolkit's Indexes panel and observe the new index card. | Card shows spinner/in-progress indicator during indexing. |
| 4 | Wait for indexing to complete successfully. | Card updates to show green checkmark or "Index is ready!" status. |
| 5 | Click on the completed index card to open details. | Index details page shows "Index is ready!" message with green indicator. |
| 6 | Observe the statistics display. | Shows: Created date, Last reindex date/time, Documents indexed count, Files reindexed, Files skipped. |
| 7 | If an index has errors, observe the error state. | Card shows error indicator; details page shows error information. |

## Expected Final State

Index card displays correct status indicator matching the actual index state (processing, ready, or error).

## Pass/Fail Criteria

**Pass:**
- In-progress state shows spinner/processing indicator
- Completed state shows green "ready" indicator
- Error state shows error indicator
- Status updates when index state changes

**Fail:**
- Missing or incorrect status indicators
- Status doesn't update when state changes
- Inconsistent indicators between card and details page
