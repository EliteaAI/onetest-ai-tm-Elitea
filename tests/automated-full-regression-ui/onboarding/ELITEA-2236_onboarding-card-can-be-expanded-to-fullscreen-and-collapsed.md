---
id: ELITEA-2236
title: "Onboarding — card can be expanded to fullscreen and collapsed with X button"
priority: high
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2236: Onboarding — card can be expanded to fullscreen and collapsed with X button

**Module:** onboarding · **Priority:** high · **Type:** functional

**Objective:** Verify that Onboarding — card can be expanded to fullscreen and collapsed with X button. Success is confirmed when verify the modal collapses and returns to the embedded card view on the main page.

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
| 1 | Log in to the application for the first time and verify the onboarding card is visible | User is authenticated and lands on the expected landing page. |
| 2 | Locate the expand/fullscreen icon in the top right corner of the onboarding card | Action completes without error and produces the expected UI state. |
| 3 | Click the expand icon | Control responds; expected next state is shown. |
| 4 | Verify the card expands to a fullscreen/enlarged modal state | Condition holds as described. |
| 5 | Verify the modal title "Onboarding tips" is displayed in the top left of the enlarged view | Condition holds as described. |
| 6 | Verify the slide content, image, title, description, and page counter are all still visible in the enlarged state | Condition holds as described. |
| 7 | Verify an X (close/collapse) button is displayed in the top right of the enlarged modal | Condition holds as described. |
| 8 | Click the X button | Control responds; expected next state is shown. |
| 9 | Verify the modal collapses and returns to the embedded card view on the main page | Condition holds as described. |

---

## Expected Final State

Verify the modal collapses and returns to the embedded card view on the main page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — card can be expanded to fullscreen and collapsed with X button.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
