---
id: ELITEA-2235
title: "Onboarding — onboarding tips card is displayed on first login starting at slide 1/48"
priority: high
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2235: Onboarding — onboarding tips card is displayed on first login starting at slide 1/48

**Module:** onboarding · **Priority:** high · **Type:** functional

**Objective:** Verify that Onboarding — onboarding tips card is displayed on first login starting at slide 1/48. Success is confirmed when verify the "your elitea workspace is ready!" banner with "jump in now!" button is visible below the card.

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
| 2 | Verify the onboarding tips card is automatically displayed in the main content area | Condition holds as described. |
| 3 | Verify the ELITEA logo is shown at the top center of the card | Condition holds as described. |
| 4 | Verify the first slide shows "Tip 1: Welcome to ELITEA" as the title | Condition holds as described. |
| 5 | Verify the description reads: "ELITEA is your AI-powered workspace where you create intelligent agents, automate workflows with pipelines, and chat with powerful AI models. Everything you need is organized in the left sidebar for easy access." | Condition holds as described. |
| 6 | Verify the Quick Action text reads: "Click the ELITEA logo (top-left) to explore all available menus." | Condition holds as described. |
| 7 | Verify the slide counter shows "1 / 48" | Condition holds as described. |
| 8 | Verify the "Your Elitea workspace is ready!" banner with "Jump in now!" button is visible below the card | Condition holds as described. |

---

## Expected Final State

Verify the "Your Elitea workspace is ready!" banner with "Jump in now!" button is visible below the card.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — onboarding tips card is displayed on first login starting at slide 1/48.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
