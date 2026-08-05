---
id: ELITEA-2304
title: "Batch edit roles for multiple selected users"
priority: high
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_users_batch_edit_roles.TestBatchEditRolesForMultipleSelectedUsers.test_batch_edit_roles_for_multiple_selected_users
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1182
---

# ELITEA-2304: Batch edit roles for multiple selected users

**Module:** settings-users-and-roles · **Priority:** high · **Type:** functional

**Objective:** Verify that Batch edit roles for multiple selected users. Success is confirmed when verify unselected users' roles remain unchanged.

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
| 2 | Select checkboxes on two or more user rows | Control responds; expected next state is shown. |
| 3 | Verify the Edit (pencil) icon in the header becomes active | Condition holds as described. |
| 4 | Click the header Edit icon | Control responds; expected next state is shown. |
| 5 | Verify the "Edit roles" dialog opens | Condition holds as described. |
| 6 | Select a new role (e.g., "viewer") | Control responds; expected next state is shown. |
| 7 | Confirm the change | Operation completes successfully; state updates and confirmation is shown. |
| 8 | Verify all selected users now show "viewer" in the Role column | Condition holds as described. |
| 9 | Verify unselected users' roles remain unchanged | Condition holds as described. |

---

## Expected Final State

Verify unselected users' roles remain unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Batch edit roles for multiple selected users.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
