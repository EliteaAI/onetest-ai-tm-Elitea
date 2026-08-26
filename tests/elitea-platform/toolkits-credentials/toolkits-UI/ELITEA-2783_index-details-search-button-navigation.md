---
id: ELITEA-2783
title: "Index Details - Search Button Navigation to Search Page"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, smoke, search, navigation]
requirements: []
---
# ELITEA-2783: Index Details - Search Button Navigation to Search Page

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional / Smoke

**Objective:** Verify "Search" button opens the Search/Test page with correct layout and functionality.

**Coverage:**
- "Search" button visible and clickable on Index Details page
- Search page opens with two-panel layout
- Breadcrumb navigation is correct
- Tooltip displays on hover

## Preconditions

- Logged in to {{base_url}}
- A toolkit with at least one completed index

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexes |
| Index | A completed index (status: "Index is ready!") |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select a toolkit → click an index card. | Index Details page opens. |
| 2 | Locate the "Search" button in the header area (next to "Run History"). | "Search" button is visible. |
| 3 | Hover over the "Search" button. | Tooltip displays "Search this index" or similar. |
| 4 | Click the "Search" button. | Search page opens in the same browser tab. |
| 5 | Verify the breadcrumb navigation. | Breadcrumb shows: "Toolkits & Indexes / [Toolkit] / [Index] / Search". |
| 6 | Observe the page layout. | Two-panel layout: "Search Settings" on left, "Results" on right. |
| 7 | Verify empty state in Search Settings panel. | Shows icon, "Choose a tool from the list to configure parameters and run the test." message, and "Select Tool" button. |

## Expected Final State

Search page displays with two-panel layout, correct breadcrumb, and "Select Tool" button in empty state.

## Pass/Fail Criteria

**Pass:**
- "Search" button visible and responds to click
- Correct tooltip on hover
- Search page opens with two-panel layout
- Breadcrumb shows full navigation path
- Empty state displays correctly

**Fail:**
- "Search" button missing or not clickable
- No tooltip or incorrect tooltip
- Wrong page layout
- Incorrect or missing breadcrumb
