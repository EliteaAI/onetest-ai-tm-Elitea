---
id: ELITEA-2255
title: "Notifications Center page loads with correct layout and header"
priority: high
type: functional
module: settings-notifications
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_notification_center_layout.TestNotificationCenterLayout.test_notification_center_page_layout_and_header
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1788"
---

# ELITEA-2255: Notifications Center page loads with correct layout and header

**Module:** settings-notifications · **Priority:** high · **Type:** functional

**Objective:** Verify that Notifications Center page loads with correct layout and header. Success is confirmed when verify the page does not remain in a permanent loading state.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Notifications | Target page/section loads successfully. |
| 2 | Verify the page header shows "Notifications Center" | Condition holds as described. |
| 3 | Verify a Search input field is present in the top right area | Condition holds as described. |
| 4 | Verify two action buttons are present in the top right area: | Condition holds as described. |
| 5 | Mark as read (envelope/mail icon) | Action completes without error and produces the expected UI state. |
| 6 | Delete (trash icon) | Operation completes successfully; state updates and confirmation is shown. |
| 7 | Verify the notification table is shown with columns: checkbox, Type (icon), Notification (text + link), Date & Time | Condition holds as described. |
| 8 | Verify the page does not remain in a permanent loading state | Condition holds as described. |

---

## Expected Final State

Verify the page does not remain in a permanent loading state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Notifications Center page loads with correct layout and header.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
