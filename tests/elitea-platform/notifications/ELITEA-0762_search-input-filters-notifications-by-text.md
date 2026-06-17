---
id: ELITEA-0762
title: "Search Input Filters Notifications by Text"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0762: Search Input Filters Notifications by Text

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the search input in the Notification Center filters the table by matching notification text, and restores results when cleared.

**Coverage:**
- Search input present in the top-right area
- Typing a keyword shows only matching notifications
- Non-matching notifications are hidden
- Clearing search input restores all notifications
- No-results state shown when search matches nothing

## Preconditions

- Logged in to {{base_url}}
- At least 3 notifications present with varied text content

## Test Data

- URL: {{base_url}}
- Search keyword (matching): "Docs" or "Altadoc" (present in at least 1 notification)
- Search keyword (non-matching): "xyz_no_match_test_string"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/notification-center | Notification Center table is displayed |
| 2 | Locate the Search input field in the top-right area | Search input is visible |
| 3 | Type 'Docs' (or another keyword present in at least 1 notification) into the search input | Table updates to show only notifications containing the search term |
| 4 | Verify notifications NOT containing the term are hidden from view | Non-matching notifications are not shown |
| 5 | Clear the search input | All notifications are shown again |
| 6 | Type 'xyz_no_match_test_string' into the search input | An appropriate empty/no-results state is displayed |

## Expected Final State

An appropriate empty/no-results state is displayed

## Pass/Fail Criteria

**Pass:**
- Table filters correctly to matching notifications only
- Clearing search restores the full list
- Empty state shown when no results match

**Fail:**
- Search has no effect on the displayed list
- Clearing search does not restore all notifications
- Matching notifications are not returned
