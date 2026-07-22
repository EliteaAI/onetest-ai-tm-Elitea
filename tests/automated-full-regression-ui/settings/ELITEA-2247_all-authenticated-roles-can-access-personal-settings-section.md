---
id: ELITEA-2247
title: "All authenticated roles can access PERSONAL settings sections"
priority: high
type: functional
module: settings
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2247: All authenticated roles can access PERSONAL settings sections

**Module:** settings · **Priority:** high · **Type:** functional

**Objective:** Verify that All authenticated roles can access PERSONAL settings sections. Success is confirmed when verify all four roles can access all three personal sections without any permission error.

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
| 1 | Log in as a user with Admin role — navigate to Personalization, Personal Tokens, Notifications and verify each loads without error | User is authenticated and lands on the expected landing page. |
| 2 | Repeat step 1 for Editor role | Action completes without error and produces the expected UI state. |
| 3 | Repeat step 1 for Viewer role | Action completes without error and produces the expected UI state. |
| 4 | Repeat step 1 for Monitor role | Action completes without error and produces the expected UI state. |
| 5 | Verify all four roles can access all three PERSONAL sections without any permission error | Condition holds as described. |

---

## Expected Final State

Verify all four roles can access all three PERSONAL sections without any permission error.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: All authenticated roles can access PERSONAL settings sections.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
