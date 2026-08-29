---
id: ELITEA-2409
title: "Create LLM Model — ID is auto-populated from Display Name"
priority: medium
type: functional
module: settings-ai-configuration
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_llm_model_id_autopopulated.TestLlmModelIdAutoPopulated.test_id_is_auto_populated_and_read_only
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1990"
---

# ELITEA-2409: Create LLM Model — ID is auto-populated from Display Name

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create LLM Model — ID is auto-populated from Display Name. Success is confirmed when verify the id field is editable if needed.

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
| 1 | Navigate to Settings → AI Configuration → click "+" → select "LLM Model" | Target page/section loads successfully. |
| 2 | Type "My Test Model" in the Display Name field | Field accepts the input and displays the entered value. |
| 3 | Verify the ID field is automatically populated (e.g., "my-test-model" or similar slug) | Condition holds as described. |
| 4 | Verify the ID field is editable if needed | Condition holds as described. |

---

## Expected Final State

Verify the ID field is editable if needed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create LLM Model — ID is auto-populated from Display Name.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
