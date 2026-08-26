---
id: ELITEA-2790
title: "Breadcrumb Navigation Throughout Toolkit-Index Flow"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, navigation, breadcrumb]
requirements: []
---
# ELITEA-2790: Breadcrumb Navigation Throughout Toolkit-Index Flow

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify breadcrumb navigation works correctly throughout the entire toolkit-index flow.

**Coverage:**
- Breadcrumb displays correct path at each level
- Clicking breadcrumb items navigates correctly
- Back navigation preserves state
- URL updates match breadcrumb

## Preconditions

- Logged in to {{base_url}}
- A toolkit with at least one index

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | "test1" (or any toolkit with indexes) |
| Index | "doc" (or any existing index) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes list page. | List page displays; breadcrumb may show "Toolkits & Indexes". |
| 2 | Click on a toolkit to open details. | Toolkit details page; breadcrumb: "Toolkits & Indexes / [Toolkit name]". |
| 3 | Click on an index card. | Index details page; breadcrumb: "Toolkits & Indexes / [Toolkit] / [Index]". |
| 4 | Click "Search" button. | Search page; breadcrumb: "Toolkits & Indexes / [Toolkit] / [Index] / Search". |
| 5 | Click the Index name in breadcrumb. | Navigates back to Index Details page. |
| 6 | Click "Run History" button. | History page; breadcrumb: "Toolkits & Indexes / [Toolkit] / [Index] / History". |
| 7 | Click the Toolkit name in breadcrumb. | Navigates back to Toolkit Details page. |
| 8 | Click "Toolkits & Indexes" in breadcrumb. | Navigates back to Toolkits list page. |
| 9 | Use browser back button from History page. | Returns to previous page (Index Details). |

## Expected Final State

All breadcrumb links navigate to correct pages, and browser back button works correctly.

## Pass/Fail Criteria

**Pass:**
- Breadcrumb shows accurate path at each level
- All breadcrumb links are clickable and navigate correctly
- Browser back button works as expected
- URL matches the current page/breadcrumb

**Fail:**
- Incorrect breadcrumb path
- Breadcrumb links don't navigate
- Browser back doesn't work
- URL mismatch
