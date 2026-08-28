---
id: ELITEA-2916
title: "Regression: Background Indexing Continues Across Navigation"
priority: high
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, toolkit-redesign, indexes, background-indexing]
requirements: []
---
# ELITEA-2916: Regression: Background Indexing Continues Across Navigation

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Regression

**Objective:** Verify an indexing operation is not interrupted or reset when the user navigates away from the Index details page and back.

**Coverage:**
- Indexing continues while the user is on another page
- Activity information is not reset by navigating away and returning

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
| 2 | Inspect the Activity view. | Indexing operation is displayed as running. |
| 3 | Navigate to the Toolkits & Indexes list while indexing is still in progress. | List page displays. |
| 4 | Open the same Toolkit. | Toolkit details page displays. |
| 5 | Open the same Index. | Index details page opens with "Activity" selected. |
| 6 | Inspect the Activity view. | Indexing is still displayed as running, or has reached the ready state if enough time has elapsed for it to complete. |
| 7 | Compare the activity information to step 2. | Activity information reflects continued progress and was not reset by the navigation. |

## Expected Final State

The indexing operation completes (or continues) exactly as it would have without the navigation away and back.

## Pass/Fail Criteria

**Pass:**
- Indexing status after returning reflects continued progress or completion, not a reset
- Activity information is consistent with uninterrupted execution

**Fail:**
- Indexing shows as reset, restarted, or stalled after navigating away and back
