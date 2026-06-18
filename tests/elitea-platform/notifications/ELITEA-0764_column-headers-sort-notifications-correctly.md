---
id: ELITEA-0764
title: "Column Headers Sort Notifications Correctly"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0764: Column Headers Sort Notifications Correctly

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify both column headers (Notification, Date&Time) are sortable and correctly reorder the table, with the sort indicator updating on each click.

**Coverage:**
- Date&Time column sorts ascending then descending
- Notification column sorts alphabetically
- Sort direction indicator (arrow) updates correctly

## Preconditions

- Logged in to {{base_url}}
- At least 5 notifications with varied dates and text

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to {{base_url}} | Notification Center table is displayed |
| 2 | Click the Date&Time column header | Rows re-sort ascending (oldest first) and sort arrow indicates ascending direction |
| 3 | Click Date&Time column header again | Rows re-sort descending (newest first) and sort arrow reverses direction |
| 4 | Click the Notification column header | Rows re-sort alphabetically by notification text and sort arrow updates accordingly |

## Expected Final State

Rows re-sort alphabetically by notification text and sort arrow updates accordingly

## Pass/Fail Criteria

**Pass:**
- Clicking each column header sorts the table correctly in both directions
- Sort direction indicator updates on each click

**Fail:**
- Column headers are not clickable or have no sort effect
- Sort order is incorrect
- Sort indicator does not update
