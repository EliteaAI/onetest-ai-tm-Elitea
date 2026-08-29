---
id: ELITEA-2305
title: "Available roles in Invite and Edit dialogs are admin, editor, and viewer"
priority: medium
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_users_roles_in_invite_and_edit_dialogs.TestUsersRolesInInviteAndEditDialogs.test_available_roles_in_invite_and_edit_dialogs
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2305: Available roles in Invite and Edit dialogs are admin, editor, and viewer

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Available roles in Invite and Edit dialogs are admin, editor, and viewer. Success is confirmed when verify the same three options: admin, editor, viewer.

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
| 2 | Click "+" to open Invite users dialog | Control responds; expected next state is shown. |
| 3 | Open the Roles dropdown — verify exactly three options: admin, editor, viewer | Target page/section loads successfully. |
| 4 | Close the dialog | Action completes without error and produces the expected UI state. |
| 5 | Click Edit on any user row — open the Roles dropdown | Control responds; expected next state is shown. |
| 6 | Verify the same three options: admin, editor, viewer | Condition holds as described. |

---

## Expected Final State

Verify the same three options: admin, editor, viewer.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Available roles in Invite and Edit dialogs are admin, editor, and viewer.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
