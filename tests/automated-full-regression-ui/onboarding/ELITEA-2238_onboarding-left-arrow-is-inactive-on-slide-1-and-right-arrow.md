---
id: ELITEA-2238
title: "Onboarding — left arrow is inactive on slide 1 and right arrow is inactive on slide 48"
priority: medium
type: functional
module: onboarding
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:onboarding]
requirements: []
automation_test_id:
  - tests.ui.onboarding.test_onboarding_tips_navigation.TestOnboardingTipsArrowBoundaries.test_arrows_inactive_at_first_and_last_slide
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1763
---

# ELITEA-2238: Onboarding — left arrow is inactive on slide 1 and right arrow is inactive on slide 48

**Module:** onboarding · **Priority:** medium · **Type:** functional

**Objective:** Verify that Onboarding — left arrow is inactive on slide 1 and right arrow is inactive on slide 48. Success is confirmed when click the right arrow (>) and verify no navigation occurs (stays on slide 48/48).

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
| 2 | Verify the left arrow (<) / Back button is visually inactive (disabled/greyed out) on slide 1/48 | Condition holds as described. |
| 3 | Click the left arrow (<) and verify no navigation occurs (stays on slide 1/48) | Control responds; expected next state is shown. |
| 4 | Click the right arrow (>) repeatedly until slide 48/48 is reached | Control responds; expected next state is shown. |
| 5 | Verify the slide counter shows "48 / 48" | Condition holds as described. |
| 6 | Verify the slide content shows "Tip 48: View Message Execution Details" | Condition holds as described. |
| 7 | Verify the right arrow (>) / Next button is visually inactive (disabled/greyed out) on slide 48/48 | Condition holds as described. |
| 8 | Click the right arrow (>) and verify no navigation occurs (stays on slide 48/48) | Control responds; expected next state is shown. |

---

## Expected Final State

Click the right arrow (>) and verify no navigation occurs (stays on slide 48/48).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — left arrow is inactive on slide 1 and right arrow is inactive on slide 48.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
