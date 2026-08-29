---
id: ELITEA-2298
title: "Delete a user via per-row Delete icon"
priority: medium
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_user_delete_via_row_icon.TestUserDeleteViaRowIcon.test_delete_user_via_row_icon
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2298: Delete a user via per-row Delete icon

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Delete a user via per-row Delete icon. Success is confirmed when reload the page — verify the user does not reappear.

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
| 1 | Navigate to Settings → Users as Admin | Target page/section loads successfully. |
| 2 | Click the trash icon in the Actions column of any user row | Control responds; expected next state is shown. |
| 3 | Verify a confirmation dialog appears | Condition holds as described. |
| 4 | Confirm deletion | Operation completes successfully; state updates and confirmation is shown. |
| 5 | Verify the user is removed from the table | Condition holds as described. |
| 6 | Reload the page — verify the user does not reappear | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Reload the page — verify the user does not reappear.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Delete a user via per-row Delete icon.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
