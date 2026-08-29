---
id: ELITEA-2295
title: "Invite users dialog opens with correct layout"
priority: medium
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_users_invite_dialog_layout.TestUsersInviteDialogLayout.test_invite_users_dialog_opens_with_correct_layout
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2295: Invite users dialog opens with correct layout

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Invite users dialog opens with correct layout. Success is confirmed when verify the "invite users" dialog opens with:.

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
| 2 | Click the "+" button | Control responds; expected next state is shown. |
| 3 | Verify the "Invite users" dialog opens with: | Condition holds as described. |
| 4 | Title "Invite users" | Action completes without error and produces the expected UI state. |
| 5 | Description: "Enter user emails(separated by comma) and select roles to define permissions for this project." | Action completes without error and produces the expected UI state. |
| 6 | Emails field (marked as required with *) | Action completes without error and produces the expected UI state. |
| 7 | Roles dropdown showing: admin, editor, viewer | Action completes without error and produces the expected UI state. |
| 8 | Close (×) button in the top right | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Close (×) button in the top right.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Invite users dialog opens with correct layout.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
