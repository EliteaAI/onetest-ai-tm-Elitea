---
id: ELITEA-0208
title: "Invalid Max Tokens Value Shows Validation Error and Is Not Saved"
priority: medium
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0208: Invalid Max Tokens Value Shows Validation Error and Is Not Saved

**Module:** Agents Studio · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that entering an invalid value in the Max Tokens field triggers a validation error and the settings are not saved.

**Coverage:**
- Validation for zero, negative, and non-numeric inputs
- Settings not saved on invalid input

## Preconditions

- Model Settings dialog is open in Custom Max Tokens mode

## Test Data

Test values: 0 (zero), -100 (negative), abc (non-numeric)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Model Settings, select Custom. | Max Tokens input is active. |
| 2 | Enter 0 in Max Tokens field, click Apply. | Validation error shown; settings not applied. |
| 3 | Enter -100, click Apply. | Validation error shown; settings not applied. |
| 4 | Enter 'abc', click Apply. | Validation error shown; settings not applied. |

## Expected Final State

Validation error shown; settings not applied.

## Pass/Fail Criteria

**Pass:**
- Each invalid value produces a visible validation error message
- Settings dialog does not close and values are not saved

**Fail:**
- Invalid values are accepted without error
- Negative or zero tokens are saved and applied
