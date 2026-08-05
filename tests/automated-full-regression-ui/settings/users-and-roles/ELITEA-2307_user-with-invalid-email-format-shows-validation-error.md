---
id: ELITEA-2307
title: "User with invalid email format shows validation error"
priority: medium
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_invite_user_invalid_email_validation.TestInviteUserInvalidEmailValidation.test_invite_user_invalid_email_validation
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1184
---

# ELITEA-2307: User with invalid email format shows validation error

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that User with invalid email format shows validation error. Success is confirmed when verify a validation error is shown below the emails field.

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
| 3 | Enter an invalid email (e.g., "notanemail" or "user@") | Field accepts the input and displays the entered value. |
| 4 | Verify a validation error is shown below the Emails field | Condition holds as described. |

---

## Expected Final State

Verify a validation error is shown below the Emails field.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: User with invalid email format shows validation error.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
