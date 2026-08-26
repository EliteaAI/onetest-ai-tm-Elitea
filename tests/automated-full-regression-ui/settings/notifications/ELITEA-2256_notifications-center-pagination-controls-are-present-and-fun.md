---
id: ELITEA-2256
title: "Notifications Center pagination controls are present and functional"
priority: medium
type: functional
module: settings-notifications
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_notification_center_pagination.TestNotificationCenterPagination.test_notification_center_pagination_controls
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1788"
---

# ELITEA-2256: Notifications Center pagination controls are present and functional

**Module:** settings-notifications · **Priority:** medium · **Type:** functional

**Objective:** Verify that Notifications Center pagination controls are present and functional. Success is confirmed when verify the page range label updates and a new set of notifications is shown.

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
| 2 | Verify pagination controls are shown at the bottom: "Rows per page" selector, page range label (e.g., "1–50 of 195"), prev/next arrows | Condition holds as described. |
| 3 | Change "Rows per page" to a different value (e.g., 10) | Action completes without error and produces the expected UI state. |
| 4 | Verify the table updates to show the selected number of rows | Condition holds as described. |
| 5 | Click the next page arrow | Control responds; expected next state is shown. |
| 6 | Verify the page range label updates and a new set of notifications is shown | Condition holds as described. |

---

## Expected Final State

Verify the page range label updates and a new set of notifications is shown.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Notifications Center pagination controls are present and functional.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
