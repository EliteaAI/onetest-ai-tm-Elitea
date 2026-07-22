---
id: ELITEA-2379
title: "Summarization instructions and target tokens persist after save and reload"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2379: Summarization instructions and target tokens persist after save and reload

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Summarization instructions and target tokens persist after save and reload. Success is confirmed when verify target summary tokens shows 300.

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
| 1 | Navigate to  Personalization → DEFAULT SUMMARIZATION | Target page/section loads successfully. |
| 2 | Enable automatic summarization | Action completes without error and produces the expected UI state. |
| 3 | Enter summarization instructions: "Summarize briefly, focus on key actions." | Field accepts the input and displays the entered value. |
| 4 | Set Target Summary Tokens to 300 | Action completes without error and produces the expected UI state. |
| 5 | Click outside to trigger autosave | Control responds; expected next state is shown. |
| 6 | Reload the page | Action completes without error and produces the expected UI state. |
| 7 | Verify Summarization Instructions shows "Summarize briefly, focus on key actions." | Condition holds as described. |
| 8 | Verify Target Summary Tokens shows 300 | Condition holds as described. |

---

## Expected Final State

Verify Target Summary Tokens shows 300.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Summarization instructions and target tokens persist after save and reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
