---
id: ELITEA-2957
title: "Regression: Stop Produces Consistent Result From Activity and Configuration"
priority: medium
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, toolkit-redesign, indexes, stop]
requirements: []
---
# ELITEA-2957: Regression: Stop Produces Consistent Result From Activity and Configuration

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Regression

**Objective:** Verify that clicking "Stop" from the Activity tab and clicking "Stop" from the Configuration tab produce the same resulting status.

**Coverage:**
- "Stop" from Activity produces the orange stopped status and "Reindex"
- "Stop" from Configuration produces the same orange stopped status and "Reindex"

## Preconditions

- Logged in to {{base_url}} with edit permissions
- Two Indexes, each with an indexing operation currently in progress

## Test Data

| Field | Value |
|-------|-------|
| Index A | Currently indexing |
| Index B | Currently indexing |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Index A's details page while its indexing operation is running. | Page opens with "Activity" selected and "Stop" displayed. |
| 2 | Click "Stop". | Indexing operation stops. |
| 3 | Inspect the status indicator and available action. | Status indicator uses the orange stopped color; "Reindex" is displayed. |
| 4 | Open Index B's details page while its indexing operation is running. | Page opens with "Activity" selected. |
| 5 | Click "Configuration". | "Configuration" tab displays with "Stop" visible. |
| 6 | Click "Stop". | Indexing operation stops. |
| 7 | Click "Activity". | "Activity" tab displays. |
| 8 | Inspect the status indicator and available action. | Status indicator uses the orange stopped color and "Reindex" is displayed, matching Index A in step 3. |

## Expected Final State

Both Indexes show the identical stopped status and "Reindex" availability, regardless of which tab "Stop" was clicked from.

## Pass/Fail Criteria

**Pass:**
- Both Indexes reach the same stopped status indicator and "Reindex" availability

**Fail:**
- The two Indexes show different status indicators, or "Reindex" is available for one but not the other
