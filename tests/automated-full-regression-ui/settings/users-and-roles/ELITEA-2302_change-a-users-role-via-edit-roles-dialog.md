---
id: ELITEA-2302
title: "Change a user's role via Edit roles dialog"
priority: medium
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_users_row_edit_roles_change.TestUsersRowEditRolesChange.test_change_roles_via_row_edit_dialog
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2302: Change a user's role via Edit roles dialog

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Change a user's role via Edit roles dialog. Success is confirmed when reload the page — verify the role change persists.

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
| 2 | Click the Edit (pencil) icon on a user with "viewer" role | Control responds; expected next state is shown. |
| 3 | In the Roles dropdown remove "viewer" by clicking the × on the chip | Action completes without error and produces the expected UI state. |
| 4 | Select "editor" from the dropdown | Control responds; expected next state is shown. |
| 5 | Confirm the change | Operation completes successfully; state updates and confirmation is shown. |
| 6 | Verify the user's Role column updates to "editor" | Condition holds as described. |
| 7 | Reload the page — verify the role change persists | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Reload the page — verify the role change persists.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Change a user's role via Edit roles dialog.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
