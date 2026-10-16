---
id: ELITEA-3958
title: "Indexes Panel Empty State and Create Index Button"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, smoke, indexes]
requirements: []
---
# ELITEA-3958: Indexes Panel Empty State and Create Index Button

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional / Smoke

**Objective:** Verify empty state message and "+ Index" button functionality in the Indexes panel.

**Coverage:**
- Empty state displays "No indexes created yet." message
- "+ Index" button is visible in empty state
- Clicking "+ Index" opens Create Index page
- Newly created index appears in the panel

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with no existing indexes OR create a new toolkit
- PgVector and Embedding Model configured at project level

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | A toolkit with zero indexes |
| Index Name | "test-index-001" |
| Branch | "main" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select a toolkit with no indexes. | Toolkit details page opens. |
| 2 | Observe the right panel (Indexes section). | Panel shows "Indexes (0)" header and "No indexes created yet." empty state message. |
| 3 | Verify "+ Index" button is visible in the empty state area. | "+ Index" button is displayed. |
| 4 | Click the "+ Index" button. | Create Index page/form opens with Name, Branch, Whitelist, Blacklist fields. |
| 5 | Enter Index Name: "test-index-001", Branch: "main". | Fields accept input. |
| 6 | Click the "Index" button to create the index. | App navigates to the new index's details page with the "Activity" tab selected by default; indexing progress shown. |
| 7 | Navigate to the toolkit details page (e.g., via breadcrumb). | Toolkit details page displays. |
| 8 | Observe the Indexes panel. | New index card "test-index-001" appears; header shows "Indexes (1)". |

## Expected Final State

Creating the index navigates to its details page with Activity selected, and the Indexes panel (once revisited) shows the new index card with header updated to "Indexes (1)".

## Pass/Fail Criteria

**Pass:**
- Empty state message displays correctly when no indexes exist
- "+ Index" button is visible and clickable
- Create Index form opens with all required fields
- New index appears in the panel after creation

**Fail:**
- Empty state message missing
- "+ Index" button not visible or not clickable
- Create Index form doesn't open
- New index doesn't appear after creation
