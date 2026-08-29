---
id: ELITEA-2296
title: "Invite a single user with a role"
priority: medium
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_users_invite_single_and_multiple.TestUsersInviteSingleAndMultiple.test_invite_users_with_role
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2296: Invite a single user with a role

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Invite a single user with a role. Success is confirmed when verify the invited user appears in the users table with "viewer" role.

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
| 2 | Click "+" | Control responds; expected next state is shown. |
| 3 | Enter a valid email address in the Emails field | Field accepts the input and displays the entered value. |
| 4 | Click the Roles dropdown and select "viewer" | Control responds; expected next state is shown. |
| 5 | Click Invite | Control responds; expected next state is shown. |
| 6 | Verify the dialog closes and a success confirmation is shown | Condition holds as described. |
| 7 | Verify the invited user appears in the Users table with "viewer" role | Condition holds as described. |

---

## Expected Final State

Verify the invited user appears in the Users table with "viewer" role.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Invite a single user with a role.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
