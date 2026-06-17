---
id: ELITEA-0765
title: "Select All Checkbox Selects All Items on Current Page Only"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0765: Select All Checkbox Selects All Items on Current Page Only

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify clicking the Select All checkbox in the table header selects all visible rows on the current page only, and does not select rows on other pages.

**Coverage:**
- Select All selects all rows on current page
- Rows on other pages remain unselected (if pagination exists)
- Clicking Select All again deselects all rows
- Manually selecting some rows then clicking Select All selects all

## Preconditions

- Logged in to {{base_url}}
- Enough notifications to span at least 2 pagination pages (if pagination is implemented)

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/notification-center | Notification Center table is displayed |
| 2 | Locate the Select All checkbox in the table column header row | Select All checkbox is visible in the header |
| 3 | Click Select All | All rows on the current page become selected |
| 4 | If pagination is present, navigate to page 2 and verify its rows | Page 2 rows are NOT selected |
| 5 | Navigate back to page 1 and click Select All again | All rows are deselected |
| 6 | Manually select 2 rows, then click Select All | All page rows become selected (partial selection overridden) |

## Expected Final State

All page rows become selected (partial selection overridden)

## Pass/Fail Criteria

**Pass:**
- Select All selects only current page rows
- Rows on other pages remain unselected
- Toggle off deselects all rows on the page

**Fail:**
- Select All selects rows across all pages
- Select All has no visual effect on rows
- Select All cannot be toggled off
