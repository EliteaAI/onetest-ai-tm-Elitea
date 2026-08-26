---
id: ELITEA-2264
title: "Search field filters notifications by text content"
priority: medium
type: functional
module: settings-notifications
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_notification_search_filter.TestNotificationSearchFilter.test_search_field_filters_notifications_by_text
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1788"
---

# ELITEA-2264: Search field filters notifications by text content

**Module:** settings-notifications · **Priority:** medium · **Type:** functional

**Objective:** Verify that Search field filters notifications by text content. Success is confirmed when verify all notifications are shown again.

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
| 2 | Type a partial text in the Search input that matches at least one notification (e.g., a bucket name) | Field accepts the input and displays the entered value. |
| 3 | Verify the notification list filters to show only matching rows | Condition holds as described. |
| 4 | Clear the Search input | Action completes without error and produces the expected UI state. |
| 5 | Verify all notifications are shown again | Condition holds as described. |

---

## Expected Final State

Verify all notifications are shown again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Search field filters notifications by text content.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
