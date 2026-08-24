---
id: ELITEA-2232
title: "Onboarding — clicking Sure lets go triggers project provisioning and displays onboarding tips slide 1/48 with configuring progress bar"
priority: medium
type: functional
module: onboarding
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:onboarding]
requirements: []
automation_test_id:
  - tests.ui.onboarding.test_onboarding_provisioning.TestOnboardingProvisioning.test_get_started_starts_provisioning_poll_and_shows_tips_with_progress_footer
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1758
---

# ELITEA-2232: Onboarding — clicking Sure lets go triggers project provisioning and displays onboarding tips slide 1/48 with configuring progress bar

**Module:** onboarding · **Priority:** medium · **Type:** functional

**Objective:** Verify that Onboarding — clicking Sure lets go triggers project provisioning and displays onboarding tips slide 1/48 with configuring progress bar. Success is confirmed when verify after loading is completed a private project apears on left menu dropdown with sidebar entites displayed.

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
| 1 | On the Welcome to Elitea! page click the "Sure, let's go!" button | Action completes without error and produces the expected UI state. |
| 2 | Verify the welcome card is replaced by the onboarding tips slide view | Condition holds as described. |
| 3 | Verify the ELITEA logo is shown at the top center of the page | Condition holds as described. |
| 4 | Verify the first slide shows "Tip 1: Welcome to ELITEA" as the title | Condition holds as described. |
| 5 | Verify the slide description reads: "ELITEA is your AI-powered workspace where you create intelligent agents, automate workflows with pipelines, and chat with powerful AI models. Everything you need is organized in the left sidebar for easy access." | Condition holds as described. |
| 6 | Verify the Quick Action text reads: "Click the ELITEA logo (top-left) to explore all available menus." | Condition holds as described. |
| 7 | Verify the slide counter shows "1 / 48" | Condition holds as described. |
| 8 | Verify a progress bar is visible at the bottom of the page with the label "Configuring Personal project..." and estimated time "about 5 min" | Condition holds as described. |
| 9 | Verify the Personal/Private project provisioning begins only now — after clicking "Sure, let's go!" — and was not running before | Condition holds as described. |
| 10 | Verify no sidebar navigation is not visible yet and no project dropdown is available while the project is still being loading | Condition holds as described. |
| 11 | Verify after loading is completed a private project apears on left menu dropdown with sidebar entites displayed | Condition holds as described. |

---

## Expected Final State

Verify after loading is completed a private project apears on left menu dropdown with sidebar entites displayed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — clicking Sure lets go triggers project provisioning and displays onboarding tips slide 1/48 with configuring progress bar.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
