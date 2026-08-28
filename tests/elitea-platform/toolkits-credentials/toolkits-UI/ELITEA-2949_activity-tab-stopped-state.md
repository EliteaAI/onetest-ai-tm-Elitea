---
id: ELITEA-2949
title: "Activity Tab — Stopped State"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, indexes, activity-tab, status]
requirements: []
---
# ELITEA-2949: Activity Tab — Stopped State

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify the Activity tab displays the stopped status indicator and "Reindex" after "Stop" is clicked while indexing is in progress, and that the same status and "Reindex" are visible from Configuration.

**Coverage:**
- Orange stopped status indicator on Activity
- Stopped-operation details displayed
- "Reindex" displayed on Activity
- Same status and "Reindex" displayed on Configuration

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An Index that is currently indexing

## Test Data

| Field | Value |
|-------|-------|
| Index | Any Index with an in-progress indexing operation |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Index details page for an Index that is currently indexing. | Page opens with "Activity" selected and "Stop" displayed. |
| 2 | Click "Stop". | Indexing operation stops. |
| 3 | Inspect the status indicator. | Status indicator uses the orange stopped color. |
| 4 | Inspect the Activity view. | Stopped-operation details are displayed. |
| 5 | Inspect the available action. | "Reindex" is displayed. |
| 6 | Click "Configuration". | "Configuration" tab displays. |
| 7 | Inspect the status indicator and available action while "Configuration" is selected. | Same orange stopped status indicator and "Reindex" are displayed. |

## Expected Final State

Both "Activity" and "Configuration" show the stopped status and "Reindex".

## Pass/Fail Criteria

**Pass:**
- Orange stopped indicator and stopped-operation details shown on "Activity"
- "Reindex" displayed on both "Activity" and "Configuration"

**Fail:**
- Wrong status color, missing stopped-operation details, or missing/incorrect action on either tab
