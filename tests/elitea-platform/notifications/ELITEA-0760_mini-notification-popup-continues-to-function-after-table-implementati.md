---
id: ELITEA-0760
title: "Mini Notification Popup Continues to Function After Table Implementation"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0760: Mini Notification Popup Continues to Function After Table Implementation

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the mini notification popup (bell icon in sidebar) still shows recent notifications and its "View all" link navigates correctly to the new table-based Notification Center.

**Coverage:**
- Mini popup opens on click and shows recent notifications or empty state
- "View all" navigates to the correct Notification Center page
- Popup closes correctly when clicking elsewhere
- No visual regressions in popup layout

## Preconditions

- Logged in to {{base_url}}

## Test Data

- URL: any page within {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | From any page in the application, click the Notifications icon in the left sidebar | Mini popup opens and displays recent notifications or 'No notifications right now' if empty |
| 2 | Verify notifications in the popup are not cut off or visually broken | Popup content is properly displayed |
| 3 | Click 'View all' in the mini popup | Page navigates to {{base_url}} and the table is displayed |
| 4 | Navigate back and reopen the popup, then click anywhere outside the popup | Popup closes correctly without error |

## Expected Final State

Popup closes correctly without error

## Pass/Fail Criteria

**Pass:**
- Popup opens and shows notifications or empty state
- "View all" navigates to the Notification Center table
- Popup closes correctly on outside click

**Fail:**
- Popup does not open
- "View all" navigates to the wrong page or throws an error
- Popup does not close or causes UI issues
