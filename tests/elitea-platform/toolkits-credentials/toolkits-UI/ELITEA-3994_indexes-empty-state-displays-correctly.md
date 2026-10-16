---
id: ELITEA-3994
title: "Indexes Section Empty State Displays Correctly"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, indexes, empty-state]
requirements: [EL-6252]
---
# ELITEA-3994: Indexes Section Empty State Displays Correctly

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Indexes section displays correct count and empty state when no indexes exist.

**Coverage:**
- Indexes section collapsed by default
- Header shows "0 indexes" when empty
- Empty state message displayed when expanded
- "+ Index" action available in expanded empty state

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with no indexes exists (or create a new toolkit)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Toolkit with zero indexes |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes from the left sidebar. | Toolkits list page displays. |
| 2 | Open a toolkit that has no indexes. | Toolkit details page opens. |
| 3 | Observe the Indexes section state on page load. | Indexes section is collapsed by default. |
| 4 | Verify the Indexes section header displays "0 indexes" or "Indexes 0". | Header shows zero count. |
| 5 | Click the Indexes section header to expand. | Indexes section expands. |
| 6 | Observe the empty state content. | Empty state message displayed (e.g., "No indexes created yet"). |
| 7 | Verify "+ Index" action button is available. | "+ Index" button visible and clickable. |
| 8 | Click "+ Index" button. | Create Index form/page opens. |

## Expected Final State

Indexes section shows "0 indexes" in header, displays empty state message when expanded, and provides "+ Index" action.

## Pass/Fail Criteria

**Pass:**
- Indexes section collapsed by default
- Header shows "0 indexes" or equivalent
- Empty state message displayed on expand
- "+ Index" action visible and functional

**Fail:**
- Indexes section expanded by default when empty
- No count or wrong count in header
- No empty state message
- "+ Index" action missing
