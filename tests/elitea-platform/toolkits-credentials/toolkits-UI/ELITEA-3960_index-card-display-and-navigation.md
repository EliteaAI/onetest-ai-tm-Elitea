---
id: ELITEA-3960
title: "Index Card Display and Navigation to Index Details"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, smoke, indexes, navigation]
requirements: []
---
# ELITEA-3960: Index Card Display and Navigation to Index Details

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional / Smoke

**Objective:** Verify index cards show correct metadata and are clickable to navigate to Index Details page.

**Coverage:**
- Index cards display name, date, indexed item count
- Cards are clickable and navigate to Index Details
- Breadcrumb shows correct navigation path
- Index status indicators display correctly

## Preconditions

- Logged in to {{base_url}}
- A toolkit with at least one existing index (completed status)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Toolkit with existing indexes |
| Index | Any completed index (e.g., "doc") |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select a toolkit with existing indexes. | Toolkit details page opens with index cards in right panel. |
| 2 | Observe the Indexes panel header. | Header shows "Indexes (N)" where N = number of indexes. |
| 3 | Observe an index card in the panel. | Card displays: index name, creation/last update date, documents indexed count. |
| 4 | Verify "+ Index" button position when indexes exist. | Button appears in the section header (not in empty state area). |
| 5 | Click on an index card. | Navigates to Index Details page. |
| 6 | Verify the breadcrumb navigation. | Breadcrumb shows: "Toolkits & Indexes / [Toolkit name] / [Index name]". |
| 7 | Observe the Index Details page structure. | Page shows: index name header, "Search" and "Run History" buttons, Created/Last reindex stats, SCHEDULE section, Configuration/Activity tabs. |

## Expected Final State

Index Details page displays with correct breadcrumb, header info, and all expected sections.

## Pass/Fail Criteria

**Pass:**
- Index cards show name, date, and count correctly
- Cards are clickable and navigate properly
- Breadcrumb displays correct path
- Index Details page shows all expected sections

**Fail:**
- Missing or incorrect metadata on cards
- Cards not clickable
- Incorrect breadcrumb path
- Missing sections on Index Details page
