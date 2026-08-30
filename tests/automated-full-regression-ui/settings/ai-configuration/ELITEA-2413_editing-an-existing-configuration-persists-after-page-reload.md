---
id: ELITEA-2413
title: "Editing an existing configuration persists after page reload"
priority: medium
type: functional
module: settings-ai-configuration
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_llm_model_edit.TestEditLlmModelConfiguration.test_edit_llm_model_display_name
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1995"
---

# ELITEA-2413: Editing an existing configuration persists after page reload

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Editing an existing configuration persists after page reload. Success is confirmed when verify the card shows "reload test model" (not the previous name).

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
| 1 | Click on an existing LLM model card and change the Display Name to "Reload Test Model" | Control responds; expected next state is shown. |
| 2 | Click Save | Control responds; expected next state is shown. |
| 3 | Reload the page | Action completes without error and produces the expected UI state. |
| 4 | Verify the card shows "Reload Test Model" (not the previous name) | Condition holds as described. |

---

## Expected Final State

Verify the card shows "Reload Test Model" (not the previous name).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Editing an existing configuration persists after page reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
