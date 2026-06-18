---
id: ELITEA-1131
title: "Clicking Failure Notification Navigates to the Correct Failed Index"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:notifications, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3716]
---
# ELITEA-1131: Clicking Failure Notification Navigates to the Correct Failed Index

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that clicking a failure notification in the Notifications panel navigates the user to the Indexes tab of the correct toolkit where the failure occurred.

## Preconditions

- A project exists and the user has Editor role or higher.
- At least one toolkit indexing failure has already occurred.
- At least one failure notification is visible in the Notifications panel.
- The current page is NOT the Indexes tab of the failed toolkit (navigate away first to validate the redirect).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate away from the toolkit page (e.g., go to the Agents or Chat section). | User is on a different page, not the Indexes tab of the failed toolkit. |
| 2 | Click the bell-icon in the top navigation bar to open the Notifications panel. | Notifications panel opens with at least one failure notification visible. |
| 3 | Note the index name referenced in the failure notification message. | Index name is identified from the notification text. |
| 4 | Click the failure notification. | Notification is clicked; the panel closes and navigation begins. |
| 5 | Verify the page that the application navigated to. | The application navigates to the Indexes tab of the toolkit that owns the failed index. The correct index entry is visible in the list. |
| 6 | Verify that no error pages or broken navigation occur. | Page loads without errors; breadcrumb or page title reflects the correct toolkit name. |

## Expected Final State

Page loads without errors; breadcrumb or page title reflects the correct toolkit name.

## Pass/Fail Criteria

- Clicking the notification redirects to the Indexes tab.
- The correct toolkit is shown (matches the notification's index name).
- No error pages or broken navigation occur.
- The failed index entry is visible in the list.
