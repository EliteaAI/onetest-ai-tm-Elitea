---
id: ELITEA-2396
title: "Edit an existing LLM model configuration"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2396: Edit an existing LLM model configuration

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Edit an existing LLM model configuration. Success is confirmed when verify the card in the llm models section reflects the updated display name.

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
| 1 | Navigate to Settings → AI Configuration → LLM Models section | Target page/section loads successfully. |
| 2 | Click on any existing LLM model card | Control responds; expected next state is shown. |
| 3 | Verify the edit form opens pre-populated with the model's current values | Condition holds as described. |
| 4 | Change the Display Name to "Autotest LLM Model Edited" | Action completes without error and produces the expected UI state. |
| 5 | Click Save | Control responds; expected next state is shown. |
| 6 | Verify the card in the LLM Models section reflects the updated Display Name | Condition holds as described. |

---

## Expected Final State

Verify the card in the LLM Models section reflects the updated Display Name.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Edit an existing LLM model configuration.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
