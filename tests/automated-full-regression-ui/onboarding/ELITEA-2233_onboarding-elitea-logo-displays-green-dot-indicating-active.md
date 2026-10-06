---
id: ELITEA-2233
title: "Onboarding — ELITEA logo displays green dot indicating active server connection"
priority: medium
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2233: Onboarding — ELITEA logo displays green dot indicating active server connection

**Module:** onboarding · **Priority:** medium · **Type:** functional

**Objective:** Verify that Onboarding — ELITEA logo displays green dot indicating active server connection. Success is confirmed when verify no red dot is shown (red dot would indicate server is updating).

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
| 1 | Log in to the application for the first time | User is authenticated and lands on the expected landing page. |
| 2 | Locate the ELITEA logo icon in the top left of the sidebar | Action completes without error and produces the expected UI state. |
| 3 | Verify a green dot is displayed above the ELITEA logo | Condition holds as described. |
| 4 | Verify no red dot is shown (red dot would indicate server is updating) | Condition holds as described. |

---

## Expected Final State

Verify no red dot is shown (red dot would indicate server is updating).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — ELITEA logo displays green dot indicating active server connection.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
