---
id: ELITEA-2918
title: "Regression: Reindex Produces Consistent Result From Activity and Configuration"
priority: medium
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, toolkit-redesign, indexes, reindex]
requirements: []
---
# ELITEA-2918: Regression: Reindex Produces Consistent Result From Activity and Configuration

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Regression

**Objective:** Verify that clicking "Reindex" from the Activity tab and clicking "Reindex" from the Configuration tab both start an indexing operation and reach the same completed status.

**Coverage:**
- "Reindex" from Activity starts indexing and reaches the ready status
- "Reindex" from Configuration starts indexing and reaches the same ready status

## Preconditions

- Logged in to {{base_url}} with edit permissions
- Two Indexes, each with no indexing operation currently running

## Test Data

| Field | Value |
|-------|-------|
| Index A | Not currently indexing |
| Index B | Not currently indexing |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Index A's details page. | Page opens with "Activity" selected and "Reindex" displayed. |
| 2 | Click "Reindex". | Indexing operation starts. |
| 3 | Inspect the status indicator. | Status indicator uses the blue processing color. |
| 4 | Wait for the operation to complete. | Status indicator changes to the green ready color. |
| 5 | Open Index B's details page. | Page opens with "Activity" selected. |
| 6 | Click "Configuration". | "Configuration" tab displays with "Reindex" visible. |
| 7 | Click "Reindex". | Indexing operation starts. |
| 8 | Click "Activity". | "Activity" tab displays. |
| 9 | Inspect the status indicator. | Status indicator uses the blue processing color. |
| 10 | Wait for the operation to complete. | Status indicator changes to the green ready color, matching Index A in step 4. |

## Expected Final State

Both Indexes reach the same ready status after "Reindex", regardless of which tab it was triggered from.

## Pass/Fail Criteria

**Pass:**
- Both Indexes show the processing color while running and the ready color once complete

**Fail:**
- The two Indexes reach different final statuses, or one fails to start indexing
