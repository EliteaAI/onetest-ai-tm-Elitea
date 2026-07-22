---
id: ELITEA-2276
title: "Empty Project Background can be saved whith toggle OFF and ON"
priority: medium
type: functional
module: settings-project-params
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2276: Empty Project Background can be saved whith toggle OFF and ON

**Module:** settings-project-params · **Priority:** medium · **Type:** functional

**Objective:** Verify that Empty Project Background can be saved whith toggle OFF and ON. Success is confirmed when verify the settings save without error.

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
| 1 | Navigate to Settings → Project Context | Target page/section loads successfully. |
| 2 | Turn the Project Context toggle OFF | Action completes without error and produces the expected UI state. |
| 3 | Clear all content from the Project Background editor | Action completes without error and produces the expected UI state. |
| 4 | Click Save | Control responds; expected next state is shown. |
| 5 | Verify the settings save without error | Condition holds as described. |
| 6 | Turn the Project Context toggle ON | Action completes without error and produces the expected UI state. |
| 7 | Clear all content from the Project Background editor | Action completes without error and produces the expected UI state. |
| 8 | Click Save | Control responds; expected next state is shown. |
| 9 | Verify the settings save without error | Condition holds as described. |

---

## Expected Final State

Verify the settings save without error.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Empty Project Background can be saved whith toggle OFF and ON.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
