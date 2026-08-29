---
id: ELITEA-2395
title: "Create a new LLM model configuration"
priority: medium
type: functional
module: settings-ai-configuration
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_llm_model_create.TestCreateLlmModelConfiguration.test_create_llm_model_and_set_as_default
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1990"
---

# ELITEA-2395: Create a new LLM model configuration

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create a new LLM model configuration. Success is confirmed when verify it can be set as default in top menu.

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
| 1 | Navigate to Settings → AI Configuration | Target page/section loads successfully. |
| 2 | Click the "+" button in the Integrations section header | Control responds; expected next state is shown. |
| 3 | Select "LLM Model" from the integration type list | Control responds; expected next state is shown. |
| 4 | Fill in required fields: | Field accepts the input and displays the entered value. |
| 5 | Display Name: "Autotest LLM Model" | Action completes without error and produces the expected UI state. |
| 6 | Name: exact model identifier (e.g., "gpt-4o") | Action completes without error and produces the expected UI state. |
| 7 | Context Window: 128000 | Action completes without error and produces the expected UI state. |
| 8 | Max Output Tokens: 16000 | Action completes without error and produces the expected UI state. |
| 9 | Credentials: select an existing credential | Action completes without error and produces the expected UI state. |
| 10 | Click Save | Control responds; expected next state is shown. |
| 11 | Verify the new model card appears under the "Other LLM  providers" section | Condition holds as described. |
| 12 | Verify the card shows: Display Name, status badge (OK · Shared or OK · Local) | Condition holds as described. |
| 13 | Verify it can be set as default in top menu. | Condition holds as described. |

---

## Expected Final State

Verify it can be set as default in top menu.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create a new LLM model configuration.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
