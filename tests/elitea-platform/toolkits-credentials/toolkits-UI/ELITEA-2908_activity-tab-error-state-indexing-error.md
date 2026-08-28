---
id: ELITEA-2908
title: "Activity Tab — Error State (Indexing Error)"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, indexes, activity-tab, status, indexing-error]
requirements: []
---
# ELITEA-2908: Activity Tab — Error State (Indexing Error)

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify the Activity tab displays the error status indicator, error details or a Run History link, and "Reindex" when the most recent indexing operation failed, and that the same status and "Reindex" are visible from Configuration. This test covers only an indexing failure, not a search-request failure (see ELITEA-2912 for search request failures).

**Coverage:**
- Red error status indicator on Activity
- Error details or a link to Run History displayed
- "Reindex" displayed on Activity
- Same status and "Reindex" displayed on Configuration

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing Index whose most recent indexing operation resulted in an error

## Test Data

| Field | Value |
|-------|-------|
| Index | Any Index with a failed indexing operation |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Index details page for an Index whose most recent indexing operation resulted in an error. | Page opens with "Activity" selected. |
| 2 | Inspect the status indicator. | Status indicator uses the red error color. |
| 3 | Inspect the Activity view. | Error details or a link to Run History is displayed. |
| 4 | Inspect the available action. | "Reindex" is displayed. |
| 5 | Click "Configuration". | "Configuration" tab displays. |
| 6 | Inspect the status indicator and available action while "Configuration" is selected. | Same red error status indicator and "Reindex" are displayed. |

## Expected Final State

Both "Activity" and "Configuration" show the error status and "Reindex".

## Pass/Fail Criteria

**Pass:**
- Red error indicator and error details/Run History link shown on "Activity"
- "Reindex" displayed on both "Activity" and "Configuration"

**Fail:**
- Wrong status color, missing error details/link, or missing/incorrect action on either tab
