---
id: ELITEA-2952
title: "Delete Index — Confirmation and Cancellation"
priority: critical
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, indexes, delete-index]
requirements: []
---
# ELITEA-2952: Delete Index — Confirmation and Cancellation

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "Delete Index" is present and visible on the Index details page, requires confirmation before deleting, that cancelling the confirmation leaves the Index untouched, and that confirming removes the Index.

**Coverage:**
- "Delete Index" action is present and visible on the Index details page
- "Delete Index" opens a confirmation modal
- Cancelling the modal makes no change
- Confirming deletes the Index

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with two existing Indexes, so one can be deleted while the other remains for comparison

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | A toolkit with Index A and Index B |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Index A's details page and inspect the available actions. | "Delete Index" is present and visible. |
| 2 | Inspect the Indexes panel count on the Toolkit details page. | Baseline count noted. |
| 3 | Click "Delete Index". | A confirmation modal is displayed; Index A is not yet deleted. |
| 4 | Click the modal's cancel action. | Modal closes; Index A still exists. |
| 5 | Inspect the Indexes panel count. | Count is unchanged from the baseline. |
| 6 | Click "Delete Index" again. | Confirmation modal is displayed. |
| 7 | Confirm the deletion using the modal's confirm action. | Modal closes; Index A is deleted. |
| 8 | Inspect the Indexes panel count. | Count has decreased by 1 and Index A no longer appears. |
| 9 | Inspect Index B. | Index B still exists and is unaffected. |

## Expected Final State

Index A no longer exists anywhere in the UI; Index B is unaffected.

## Pass/Fail Criteria

**Pass:**
- "Delete Index" is present and visible
- "Delete Index" requires confirmation
- Cancel makes no change
- Confirm deletes the Index and decrements the count
- The sibling Index is unaffected

**Fail:**
- "Delete Index" is missing from the page
- Deletion occurs without confirmation
- Cancel still deletes or alters the Index
- Confirm does not delete the Index or the count does not update
- The sibling Index is affected
