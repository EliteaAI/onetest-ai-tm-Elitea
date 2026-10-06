---
id: ELITEA-2234
title: "Onboarding — bell notification icon shows red badge/dot on first login"
priority: high
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2234: Onboarding — bell notification icon shows red badge/dot on first login

**Module:** onboarding · **Priority:** high · **Type:** functional

**Objective:** Verify that Onboarding — bell notification icon shows red badge/dot on first login. Success is confirmed when verify notifications modal closes.

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
| 1 | Log in to private project of the application for the first time | User is authenticated and lands on the expected landing page. |
| 2 | Locate the bell (notification) icon in the top right area of the sidebar header | Action completes without error and produces the expected UI state. |
| 3 | Verify the bell icon is visible | Condition holds as described. |
| 4 | Verify red badge/dot is displayed above the bell icon | Condition holds as described. |
| 5 | Click the red dop observe a modal opens with "Project was successfully created" | Control responds; expected next state is shown. |
| 6 | Click to "X" button | Control responds; expected next state is shown. |
| 7 | Verify Notifications modal closes | Condition holds as described. |

---

## Expected Final State

Verify Notifications modal closes.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — bell notification icon shows red badge/dot on first login.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
