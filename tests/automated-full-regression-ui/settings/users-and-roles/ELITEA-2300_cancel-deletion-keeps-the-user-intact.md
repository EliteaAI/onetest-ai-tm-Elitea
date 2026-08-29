---
id: ELITEA-2300
title: "Cancel deletion keeps the user intact"
priority: high
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_user_delete_cancel_keeps_user.TestUserDeleteCancelKeepsUser.test_cancel_deletion_keeps_user_intact
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2300: Cancel deletion keeps the user intact

**Module:** settings-users-and-roles · **Priority:** high · **Type:** functional

**Objective:** Verify that Cancel deletion keeps the user intact. Success is confirmed when verify the user remains in the table unchanged.

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
| 2 | Click the trash icon on any user row | Control responds; expected next state is shown. |
| 3 | Verify a confirmation dialog appears | Condition holds as described. |
| 4 | Click Cancel / close the dialog | Control responds; expected next state is shown. |
| 5 | Verify the user remains in the table unchanged | Condition holds as described. |

---

## Expected Final State

Verify the user remains in the table unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Cancel deletion keeps the user intact.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
