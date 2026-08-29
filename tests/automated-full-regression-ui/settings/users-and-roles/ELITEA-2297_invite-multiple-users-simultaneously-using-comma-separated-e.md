---
id: ELITEA-2297
title: "Invite multiple users simultaneously using comma-separated emails"
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

# ELITEA-2297: Invite multiple users simultaneously using comma-separated emails

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Invite multiple users simultaneously using comma-separated emails. Success is confirmed when verify both users appear in the users table with the assigned role.

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
| 3 | Enter two email addresses separated by a comma (e.g., "user1@test.com, user2@test.com") | Field accepts the input and displays the entered value. |
| 4 | Select a role (e.g., "editor") | Control responds; expected next state is shown. |
| 5 | Click Invite | Control responds; expected next state is shown. |
| 6 | Verify both users appear in the Users table with the assigned role | Condition holds as described. |

---

## Expected Final State

Verify both users appear in the Users table with the assigned role.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Invite multiple users simultaneously using comma-separated emails.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
