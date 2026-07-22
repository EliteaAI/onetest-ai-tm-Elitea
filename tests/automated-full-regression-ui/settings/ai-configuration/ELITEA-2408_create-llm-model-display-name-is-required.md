---
id: ELITEA-2408
title: "Create LLM Model — Display Name is required"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2408: Create LLM Model — Display Name is required

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create LLM Model — Display Name is required. Success is confirmed when verify the save button is disabled and it is not possible to create a new model.

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
| 2 | Leave Display Name empty, fill all other required fields | Action completes without error and produces the expected UI state. |
| 3 | Verify the Save button is disabled and it is not possible to create a new model | Condition holds as described. |
| 4 | Repeat steps 2-3 for Name (model identifier) | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Repeat steps 2-3 for Name (model identifier).

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create LLM Model — Display Name is required.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
