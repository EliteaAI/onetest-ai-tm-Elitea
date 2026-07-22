---
id: ELITEA-2376
title: "Max Context Tokens and Preserve Recent Messages values persist after save and reload"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2376: Max Context Tokens and Preserve Recent Messages values persist after save and reload

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Max Context Tokens and Preserve Recent Messages values persist after save and reload. Success is confirmed when verify max context tokens shows 32000 and preserve recent messages shows 10.

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
| 2 | Set Max Context Tokens to 32000 | Action completes without error and produces the expected UI state. |
| 3 | Set Preserve Recent Messages to 10 | Action completes without error and produces the expected UI state. |
| 4 | Click somewhere on ui to trigger autosave | Control responds; expected next state is shown. |
| 5 | Reload the page | Action completes without error and produces the expected UI state. |
| 6 | Verify Max Context Tokens shows 32000 and Preserve Recent Messages shows 10 | Condition holds as described. |

---

## Expected Final State

Verify Max Context Tokens shows 32000 and Preserve Recent Messages shows 10.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Max Context Tokens and Preserve Recent Messages values persist after save and reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
