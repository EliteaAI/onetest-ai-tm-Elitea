---
id: ELITEA-2919
title: "Regression: Multiple Indexes Under One Toolkit Remain Independent"
priority: medium
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, toolkit-redesign, indexes, multi-index]
requirements: []
---
# ELITEA-2919: Regression: Multiple Indexes Under One Toolkit Remain Independent

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Regression

**Objective:** Verify that reindexing one Index under a toolkit does not change the status or activity information of a sibling Index under the same toolkit.

**Coverage:**
- Sibling Index status is unaffected while the other Index is reindexing
- Sibling Index status is unaffected after the other Index completes

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with two existing Indexes, referred to as Index A and Index B

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Toolkit with Index A and Index B, neither currently indexing |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Index A's details page. | Page opens with "Activity" selected and "Reindex" displayed. |
| 2 | Click "Reindex". | Indexing operation starts for Index A. |
| 3 | Inspect Index A's status indicator. | Status indicator uses the blue processing color. |
| 4 | Navigate to Index B's details page. | Page opens with "Activity" selected. |
| 5 | Inspect Index B's status indicator and activity information. | Status and activity information are unchanged from before Index A's reindex was started. |
| 6 | Navigate back to Index A's details page and wait for its operation to complete. | Status indicator changes to the green ready color. |
| 7 | Navigate to Index B's details page again. | Page opens. |
| 8 | Inspect Index B's status indicator and activity information. | Status and activity information remain unchanged. |

## Expected Final State

Index B's status and activity information are identical before and after Index A's reindex operation.

## Pass/Fail Criteria

**Pass:**
- Index B's status/activity information never changes as a result of Index A's reindex

**Fail:**
- Index B's status or activity information changes, is overwritten, or reflects Index A's operation
