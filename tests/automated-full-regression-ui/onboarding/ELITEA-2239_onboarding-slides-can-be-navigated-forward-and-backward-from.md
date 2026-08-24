---
id: ELITEA-2239
title: "Onboarding — slides can be navigated forward and backward from the enlarged/fullscreen state"
priority: medium
type: functional
module: onboarding
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:onboarding]
requirements: []
automation_test_id:
  - tests.ui.onboarding.test_onboarding_tips_navigation.TestOnboardingTipsFullscreenNavigation.test_navigate_forward_and_backward_in_fullscreen
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1763
---

# ELITEA-2239: Onboarding — slides can be navigated forward and backward from the enlarged/fullscreen state

**Module:** onboarding · **Priority:** medium · **Type:** functional

**Objective:** Verify that Onboarding — slides can be navigated forward and backward from the enlarged/fullscreen state. Success is confirmed when verify navigation is consistent with the same behavior as in the collapsed card view.

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
| 1 | Log in to the application for the first time and verify the onboarding card is at slide 1/48 | User is authenticated and lands on the expected landing page. |
| 2 | Click the expand icon to open the enlarged fullscreen view | Control responds; expected next state is shown. |
| 3 | Verify the slide counter shows "1 / 48" in the enlarged state | Condition holds as described. |
| 4 | Click the right arrow (>) in the enlarged view | Control responds; expected next state is shown. |
| 5 | Verify the slide counter advances to "2 / 48" and slide content updates | Condition holds as described. |
| 6 | Click the right arrow (>) again to advance to slide 3/48 | Control responds; expected next state is shown. |
| 7 | Click the left arrow (<) in the enlarged view | Control responds; expected next state is shown. |
| 8 | Verify the slide counter returns to "2 / 48" and the previous slide content is shown | Condition holds as described. |
| 9 | Verify navigation is consistent with the same behavior as in the collapsed card view | Condition holds as described. |

---

## Expected Final State

Verify navigation is consistent with the same behavior as in the collapsed card view.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — slides can be navigated forward and backward from the enlarged/fullscreen state.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
