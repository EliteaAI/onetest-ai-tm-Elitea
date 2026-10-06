---
id: ELITEA-2231
title: "Onboarding — Welcome to Elitea page is displayed on first login with Sure lets go button and no project loading yet"
priority: medium
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2231: Onboarding — Welcome to Elitea page is displayed on first login with Sure lets go button and no project loading yet

**Module:** onboarding · **Priority:** medium · **Type:** functional

**Objective:** Verify that Onboarding — Welcome to Elitea page is displayed on first login with Sure lets go button and no project loading yet. Success is confirmed when verify the personal/private project has not yet started loading at this point — project provisioning does not begin until the user clicks "sure, let's go!".

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
| 1 | Log in to the application for the first time with a new user account | User is authenticated and lands on the expected landing page. |
| 2 | Verify a full-screen welcome page is displayed with the ELITEA logo at the top center | Condition holds as described. |
| 3 | Verify the page title reads "Welcome to Elitea!" | Condition holds as described. |
| 4 | Verify a card is displayed in the center of the page with the greeting "Hello, [Username]!" (e.g. "Hello, Mariam Test!") | Condition holds as described. |
| 5 | Verify the card body text reads: "We're setting up your personal workspace — it'll be ready in about 5 minutes. While we work our magic, take a quick tour through our onboarding slides!" | Condition holds as described. |
| 6 | Verify the secondary text reads: "Ready to explore Elitea's smart tools and tips?" | Condition holds as described. |
| 7 | Verify a "Sure, let's go!" button is displayed inside the card | Condition holds as described. |
| 8 | Verify no sidebar navigation is visible at this stage (no left panel, no project dropdown) | Condition holds as described. |
| 9 | Verify the Personal/Private project has NOT yet started loading at this point — project provisioning does not begin until the user clicks "Sure, let's go!" | Condition holds as described. |

---

## Expected Final State

Verify the Personal/Private project has NOT yet started loading at this point — project provisioning does not begin until the user clicks "Sure, let's go!".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — Welcome to Elitea page is displayed on first login with Sure lets go button and no project loading yet.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
