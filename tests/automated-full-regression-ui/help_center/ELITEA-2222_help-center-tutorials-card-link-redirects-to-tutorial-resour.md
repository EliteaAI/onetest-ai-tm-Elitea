---
id: ELITEA-2222
title: "Help Center — Tutorials card link redirects to tutorial resource"
priority: medium
type: functional
module: help-center
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:help-center]
requirements: []
---

# ELITEA-2222: Help Center — Tutorials card link redirects to tutorial resource

**Module:** help-center · **Priority:** medium · **Type:** functional

**Objective:** Verify that Help Center — Tutorials card link redirects to tutorial resource. Success is confirmed when verify the target page loads without errors.

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
| 1 | Navigate to Help Center | Target page/section loads successfully. |
| 2 | Locate the TUTORIALS card (green icon, subtitle: "Step-by-step guides and use cases") | Action completes without error and produces the expected UI state. |
| 3 | Verify links displayed: e.g. Course: AI-Based EliteA Platform, How to create an Agent, How to create a Pipeline, More... | Condition holds as described. |
| 4 | Click the "How to create an Agent" link | Control responds; expected next state is shown. |
| 5 | Verify the user is redirected to the correct tutorial page | Condition holds as described. |
| 6 | Verify the target page loads without errors | Condition holds as described. |

---

## Expected Final State

Verify the target page loads without errors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Help Center — Tutorials card link redirects to tutorial resource.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
