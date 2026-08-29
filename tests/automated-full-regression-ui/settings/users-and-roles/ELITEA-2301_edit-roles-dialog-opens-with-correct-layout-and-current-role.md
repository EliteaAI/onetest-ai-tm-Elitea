---
id: ELITEA-2301
title: "Edit roles dialog opens with correct layout and current role pre-selected"
priority: medium
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_users_row_edit_roles_dialog_layout.TestUsersRowEditRolesDialogLayout.test_row_edit_roles_dialog_layout_and_current_role
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2301: Edit roles dialog opens with correct layout and current role pre-selected

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Edit roles dialog opens with correct layout and current role pre-selected. Success is confirmed when verify the "edit roles" dialog opens with:.

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
| 2 | Click the Edit (pencil) icon on any user row | Control responds; expected next state is shown. |
| 3 | Verify the "Edit roles" dialog opens with: | Condition holds as described. |
| 4 | Title "Edit roles" | Action completes without error and produces the expected UI state. |
| 5 | Description: "Select the roles to define permissions for this project." | Action completes without error and produces the expected UI state. |
| 6 | Roles multi-select dropdown showing the user's current role as a chip (e.g., "editor ×") | Action completes without error and produces the expected UI state. |
| 7 | Currently assigned role shown with a checkmark in the dropdown list | Action completes without error and produces the expected UI state. |
| 8 | Close (×) button in the top right | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Close (×) button in the top right.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Edit roles dialog opens with correct layout and current role pre-selected.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
