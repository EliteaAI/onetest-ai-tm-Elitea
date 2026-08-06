---
id: ELITEA-2391
title: "Max Context Tokens does not accept non-numeric or negative values"
priority: medium
type: functional
module: settings-user-profile
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_context_management_toggle.TestContextManagementToggle.test_max_context_tokens_rejects_non_numeric_and_negative_input
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1249
---

# ELITEA-2391: Max Context Tokens does not accept non-numeric or negative values

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Max Context Tokens does not accept non-numeric or negative values. Success is confirmed when verify no validation error is shown.

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
| 1 | Navigate to Personalization → DEFAULT CONTEXT MANAGEMENT | Target page/section loads successfully. |
| 2 | Clear Max Context Tokens and enter "abc" | Action completes without error and produces the expected UI state. |
| 3 | Verify the input is rejected | Condition holds as described. |
| 4 | Enter "-100" | Field accepts the input and displays the entered value. |
| 5 | Verify the input is rejected | Condition holds as described. |
| 6 | Enter a valid value (e.g., 64000) | Field accepts the input and displays the entered value. |
| 7 | Verify no validation error is shown | Condition holds as described. |

---

## Expected Final State

Verify no validation error is shown.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Max Context Tokens does not accept non-numeric or negative values.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
