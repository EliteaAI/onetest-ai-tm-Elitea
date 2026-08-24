---
id: ELITEA-2237
title: "Onboarding — slides can be navigated forward using the Next arrow"
priority: medium
type: functional
module: onboarding
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:onboarding]
requirements: []
automation_test_id:
  - tests.ui.onboarding.test_onboarding_tips_navigation.TestOnboardingTipsForwardNavigation.test_next_arrow_advances_slides
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1763
---

# ELITEA-2237: Onboarding — slides can be navigated forward using the Next arrow

**Module:** onboarding · **Priority:** medium · **Type:** functional

**Objective:** Verify that Onboarding — slides can be navigated forward using the Next arrow. Success is confirmed when verify the counter advances to "3 / 48" and new tip content is shown.

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
| 2 | Verify the right arrow (>) / Next button is active and clickable | Condition holds as described. |
| 3 | Click the right arrow (>) | Control responds; expected next state is shown. |
| 4 | Verify the slide counter advances to "2 / 48" | Condition holds as described. |
| 5 | Verify the slide content updates to "Tip 2: Navigate the Sidebar" | Condition holds as described. |
| 6 | Verify the description for slide 2 is displayed correctly | Condition holds as described. |
| 7 | Click the right arrow (>) again | Control responds; expected next state is shown. |
| 8 | Verify the counter advances to "3 / 48" and new tip content is shown | Condition holds as described. |

---

## Expected Final State

Verify the counter advances to "3 / 48" and new tip content is shown.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — slides can be navigated forward using the Next arrow.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
