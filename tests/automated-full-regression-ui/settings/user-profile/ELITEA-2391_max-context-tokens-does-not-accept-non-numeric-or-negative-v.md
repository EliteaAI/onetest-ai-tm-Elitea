---
id: ELITEA-2391
title: "DEPRECATED — Max Context Tokens does not accept non-numeric or negative values"
priority: medium
type: functional
module: settings-user-profile
status: deprecated
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: [EliteaAI/elitea_issues#6898]
---

# ELITEA-2391: DEPRECATED — Max Context Tokens does not accept non-numeric or negative values

**Deprecation note (2026-11-12):** The numeric "Max Context Tokens" input was removed per EliteaAI/elitea_issues#6898, replaced with a Balanced/Full radio control. Numeric input validation no longer applies — a radio control has no equivalent non-numeric/negative-value failure mode. No rewrite target identified; recommend formal deprecation in `index.json`.

Original content retained below for reference only — do not execute.

---

~~**Objective:** Verify that Max Context Tokens does not accept non-numeric or negative values. Success is confirmed when verify no validation error is shown.~~

---

## Preconditions (original, no longer applicable)

- User is logged in to the Elitea platform.

---

## Test Data (original, no longer applicable)

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps (original, no longer applicable)

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

## Expected Final State (original, no longer applicable)

Verify no validation error is shown.

---

## Pass/Fail Criteria (original, no longer applicable)

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Max Context Tokens does not accept non-numeric or negative values.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
