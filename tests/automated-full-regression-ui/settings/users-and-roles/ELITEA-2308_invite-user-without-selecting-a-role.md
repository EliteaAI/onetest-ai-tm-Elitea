---
id: ELITEA-2308
title: "Invite user without selecting a role"
priority: medium
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2308: Invite user without selecting a role

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Invite user without selecting a role. Success is confirmed when verify invite button is disabled.

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
| 3 | Enter a valid email address | Field accepts the input and displays the entered value. |
| 4 | Leave the Roles dropdown empty | Action completes without error and produces the expected UI state. |
| 5 | Verify INvite button is disabled | Condition holds as described. |

---

## Expected Final State

Verify INvite button is disabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Invite user without selecting a role.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
