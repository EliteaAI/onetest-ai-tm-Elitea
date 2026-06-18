---
id: ELITEA-0759
title: "Bulk Delete Does Not Remove Unintended Notifications Across Pages"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0759: Bulk Delete Does Not Remove Unintended Notifications Across Pages

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify bulk Delete only removes the explicitly selected notifications and does not accidentally delete notifications on other pages.

**Coverage:**
- Only selected notifications are deleted
- Notifications on other pages are unaffected
- No mass deletion occurs when a subset is selected

## Preconditions

- Logged in to {{base_url}}
- Multiple pages of notifications (enough to span at least 2 pages)

## Test Data

- URL: {{base_url}}
- Select exactly 3 specific notifications on page 1 before deleting

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to {{base_url}} | Notification Center table is displayed with pagination |
| 2 | Note the total notification count visible in the pagination indicator | Total count is noted (e.g., 45) |
| 3 | Select 3 specific notifications on page 1 — note their text/timestamps | 3 rows are selected |
| 4 | Click Delete and confirm the deletion | Deletion is triggered |
| 5 | Verify only the 3 selected notifications are removed from the table | Exactly 3 rows are gone |
| 6 | Verify the total count decreased by exactly 3 | Total count is now original minus 3 |
| 7 | Navigate to page 2 (and beyond if applicable) and verify no unintended notifications were deleted | All other pages have their notifications intact |

## Expected Final State

All other pages have their notifications intact

## Pass/Fail Criteria

**Pass:**
- Exactly 3 notifications are removed
- Total count decreases by 3
- All other notifications across all pages remain intact

**Fail:**
- More than 3 notifications are deleted
- Notifications on other pages are removed
- Total count does not match expected value
