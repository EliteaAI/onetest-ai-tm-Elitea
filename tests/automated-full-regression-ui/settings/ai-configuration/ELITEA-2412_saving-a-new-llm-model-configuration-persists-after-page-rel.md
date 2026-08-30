---
id: ELITEA-2412
title: "Saving a new LLM model configuration persists after page reload"
priority: medium
type: functional
module: settings-ai-configuration
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_llm_model_create.TestCreateLlmModelConfiguration.test_create_llm_model_and_set_as_default
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1995"
---

# ELITEA-2412: Saving a new LLM model configuration persists after page reload

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Saving a new LLM model configuration persists after page reload. Success is confirmed when verify "persist test model" card is still present in the llm models section.

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
| 1 | Create a new LLM model: Display Name "Persist Test Model", Name "gpt-4o", valid credentials | Operation completes successfully; state updates and confirmation is shown. |
| 2 | Click Save — verify the card appears in the LLM Models section | Control responds; expected next state is shown. |
| 3 | Reload the page | Action completes without error and produces the expected UI state. |
| 4 | Verify "Persist Test Model" card is still present in the LLM Models section | Condition holds as described. |

---

## Expected Final State

Verify "Persist Test Model" card is still present in the LLM Models section.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Saving a new LLM model configuration persists after page reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
