---
id: ELITEA-2906
title: "Activity Tab — Ready Status Matches Between Activity and Configuration"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, indexes, activity-tab, status]
requirements: []
---
# ELITEA-2906: Activity Tab — Ready Status Matches Between Activity and Configuration

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that once an indexing operation completes successfully, the green ready status indicator and "Reindex" action shown on the Activity tab are also shown identically on the Configuration tab.

**Coverage:**
- Green ready status indicator on Activity
- "Reindex" displayed on Activity
- Same status and "Reindex" displayed on Configuration

## Preconditions

- Logged in to {{base_url}} with edit permissions
- An existing Index whose most recent indexing operation completed successfully

## Test Data

| Field | Value |
|-------|-------|
| Index | Any Index with a successfully completed indexing operation |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Index details page for an Index whose most recent indexing operation completed successfully. | Page opens with "Activity" selected. |
| 2 | Inspect the status indicator. | Status indicator uses the green ready color. |
| 3 | Inspect the available action. | "Reindex" is displayed. |
| 4 | Click "Configuration". | "Configuration" tab displays. |
| 5 | Inspect the status indicator and available action while "Configuration" is selected. | Same green ready status indicator and "Reindex" are displayed. |

## Expected Final State

Both "Activity" and "Configuration" show the identical ready status and "Reindex" action.

## Pass/Fail Criteria

**Pass:**
- Green ready indicator shown on "Activity"
- Same indicator and "Reindex" displayed on "Configuration"

**Fail:**
- Status indicator or action differs between "Activity" and "Configuration"
- "Reindex" missing from either tab
