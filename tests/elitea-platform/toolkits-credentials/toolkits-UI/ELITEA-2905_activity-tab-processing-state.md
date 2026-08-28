---
id: ELITEA-2905
title: "Activity Tab — Processing State"
priority: critical
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, indexes, activity-tab, status]
requirements: []
---
# ELITEA-2905: Activity Tab — Processing State

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Activity tab displays the processing status indicator and "Stop" while an indexing operation is running, and that the same status and "Stop" are visible from Configuration.

**Coverage:**
- Blue processing status indicator on Activity
- Activity/progress information displayed
- "Stop" displayed on Activity
- Same status and "Stop" displayed on Configuration

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit that supports indexing and has valid source data available

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any indexable toolkit with valid source data |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a new Index on the toolkit. | Index details page opens with "Activity" selected. |
| 2 | Inspect the status indicator while indexing is in progress. | Status indicator uses the blue processing color. |
| 3 | Inspect the Activity view. | Current activity/progress information is displayed. |
| 4 | Inspect the available action. | "Stop" is displayed. |
| 5 | Click "Configuration". | "Configuration" tab displays. |
| 6 | Inspect the status indicator and available action while "Configuration" is selected. | Same blue processing status indicator and "Stop" are displayed. |

## Expected Final State

The Index is actively indexing; both "Activity" and "Configuration" show the processing status and "Stop".

## Pass/Fail Criteria

**Pass:**
- Blue processing indicator and progress information shown on "Activity"
- "Stop" displayed on both "Activity" and "Configuration"

**Fail:**
- Wrong status color, missing progress information, or missing/incorrect action on either tab
