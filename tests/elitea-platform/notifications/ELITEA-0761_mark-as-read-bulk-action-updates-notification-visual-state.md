---
id: ELITEA-0761
title: "Mark as Read Bulk Action Updates Notification Visual State"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0761: Mark as Read Bulk Action Updates Notification Visual State

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that selecting notifications and using the Mark as read bulk action updates those notifications to a read state, persists after page refresh, and does not cause data loss.

**Coverage:**
- Unread notifications have a visually distinct state
- Selecting notifications and clicking Mark as read changes their visual style to read
- No notifications are accidentally deleted
- Read state persists after page refresh

## Preconditions

- Logged in to {{base_url}}
- At least 2 notifications in an unread visual state (distinct styling from read ones)

## Test Data

- URL: {{base_url}}
- Select 2 unread notifications

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to {{base_url}} | Notification Center table is displayed |
| 2 | Verify at least 2 notifications appear in an unread visual state (e.g., bold text, different background) | Unread notifications are visually distinct from read ones |
| 3 | Select 2 unread notifications via their checkboxes | Both rows are selected and bulk actions activate |
| 4 | Click Mark as read in the bulk actions area | Action is triggered |
| 5 | Verify the 2 selected notifications display a read visual style | Visual change from unread to read state is visible |
| 6 | Verify no notifications were accidentally deleted (total count is unchanged) | Total notification count is the same as before |
| 7 | Verify bulk action area resets (checkboxes deselected, buttons disabled) | No rows are selected after action |
| 8 | Refresh the page and verify the 2 notifications remain in read state | Read state persists after page refresh |

## Expected Final State

Read state persists after page refresh

## Pass/Fail Criteria

**Pass:**
- Marked notifications change to read visual state
- State persists after page refresh
- No unintended deletions occur

**Fail:**
- No visual change after Mark as read
- State does not persist after refresh
- Notifications are deleted instead of marked
