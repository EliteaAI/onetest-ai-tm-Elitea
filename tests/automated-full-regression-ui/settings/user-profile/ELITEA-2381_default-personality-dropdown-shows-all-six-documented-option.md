---
id: ELITEA-2381
title: "Default Personality dropdown shows all six documented options"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2381: Default Personality dropdown shows all six documented options

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Default Personality dropdown shows all six documented options. Success is confirmed when verify the default personality dropdown shows "nerdy".

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
| 1 | Navigate to Personalization → GENERAL section | Target page/section loads successfully. |
| 2 | Click the Default Personality dropdown | Control responds; expected next state is shown. |
| 3 | Verify the following six options are listed: | Condition holds as described. |
| 4 | Generic | Action completes without error and produces the expected UI state. |
| 5 | QA | Action completes without error and produces the expected UI state. |
| 6 | Nerdy | Action completes without error and produces the expected UI state. |
| 7 | Quirky | Action completes without error and produces the expected UI state. |
| 8 | Cynical | Action completes without error and produces the expected UI state. |
| 9 | None | Action completes without error and produces the expected UI state. |
| 10 | Bare | Action completes without error and produces the expected UI state. |
| 11 | Select a different personality (e.g., "Nerdy") | Control responds; expected next state is shown. |
| 12 | Click outside to trigger autosave | Control responds; expected next state is shown. |
| 13 | Verify the Default Personality dropdown shows "Nerdy" | Condition holds as described. |

---

## Expected Final State

Verify the Default Personality dropdown shows "Nerdy".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Default Personality dropdown shows all six documented options.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
