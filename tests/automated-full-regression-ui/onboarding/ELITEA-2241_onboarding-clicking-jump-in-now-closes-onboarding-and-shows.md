---
id: ELITEA-2241
title: "Onboarding — clicking \"Jump in now!\" closes onboarding and shows default project page"
priority: medium
type: functional
module: onboarding
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:onboarding]
requirements: []
automation_test_id:
  - tests.ui.onboarding.test_onboarding_jump_in.TestOnboardingJumpIn.test_jump_in_now_closes_onboarding_and_shows_default_project_page
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1758
---

# ELITEA-2241: Onboarding — clicking \"Jump in now!\" closes onboarding and shows default project page

**Module:** onboarding · **Priority:** medium · **Type:** functional

**Objective:** Verify that Onboarding — clicking "Jump in now!" closes onboarding and shows default project page. Success is confirmed when verify the onboarding card is no longer shown on the screen.

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
| 1 | Log in to the application for the first time and verify the onboarding card is displayed | User is authenticated and lands on the expected landing page. |
| 2 | Locate the "Your Elitea workspace is ready!" banner at the bottom of the page | Action completes without error and produces the expected UI state. |
| 3 | Verify the "Jump in now!" button is visible and styled with a teal/green color | Condition holds as described. |
| 4 | Click the "Jump in now!" button | Control responds; expected next state is shown. |
| 5 | Verify the onboarding card is dismissed/closed | Condition holds as described. |
| 6 | Verify the user is navigated to the default project page (e.g., Chats page) | Condition holds as described. |
| 7 | Verify the full sidebar navigation is displayed and functional | Condition holds as described. |
| 8 | Verify the onboarding card is no longer shown on the screen | Condition holds as described. |

---

## Expected Final State

Verify the onboarding card is no longer shown on the screen.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — clicking "Jump in now!" closes onboarding and shows default project page.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
