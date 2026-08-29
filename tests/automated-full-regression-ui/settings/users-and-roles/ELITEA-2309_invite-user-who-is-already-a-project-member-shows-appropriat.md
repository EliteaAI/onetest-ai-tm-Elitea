---
id: ELITEA-2309
title: "Invite user who is already a project member shows appropriate error"
priority: medium
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_users_invite_existing_member_error.TestUsersInviteExistingMemberError.test_invite_existing_project_member_shows_error
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2309: Invite user who is already a project member shows appropriate error

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Invite user who is already a project member shows appropriate error. Success is confirmed when verify no duplicate entry appears in the table.

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
| 2 | Note the email of an existing project member | Action completes without error and produces the expected UI state. |
| 3 | Click "+" and enter the existing member's email | Control responds; expected next state is shown. |
| 4 | Select any role and click Invite | Control responds; expected next state is shown. |
| 5 | Verify an error or warning is shown indicating the user is already a member | Condition holds as described. |
| 6 | Verify no duplicate entry appears in the table | Condition holds as described. |

---

## Expected Final State

Verify no duplicate entry appears in the table.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Invite user who is already a project member shows appropriate error.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
