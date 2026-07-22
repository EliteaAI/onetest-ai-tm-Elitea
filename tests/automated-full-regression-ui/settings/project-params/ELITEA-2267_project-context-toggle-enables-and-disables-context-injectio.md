---
id: ELITEA-2267
title: "Project Context toggle enables and disables context injection"
priority: high
type: functional
module: settings-project-params
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2267: Project Context toggle enables and disables context injection

**Module:** settings-project-params · **Priority:** high · **Type:** functional

**Objective:** Verify that Project Context toggle enables and disables context injection. Success is confirmed when verify the toggle is saved as on.

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
| 2 | Verify the toggle is ON by default | Condition holds as described. |
| 3 | Click the toggle to turn it OFF | Control responds; expected next state is shown. |
| 4 | Click Save | Control responds; expected next state is shown. |
| 5 | Navigate away and back to Settings → Project Context | Target page/section loads successfully. |
| 6 | Verify the toggle remains OFF after save and reload | Condition holds as described. |
| 7 | Toggle back ON — click Save | Action completes without error and produces the expected UI state. |
| 8 | Verify the toggle is saved as ON | Condition holds as described. |

---

## Expected Final State

Verify the toggle is saved as ON.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Project Context toggle enables and disables context injection.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
