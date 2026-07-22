---
id: ELITEA-2398
title: "Create a new Embedding Model configuration"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2398: Create a new Embedding Model configuration

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create a new Embedding Model configuration. Success is confirmed when verify the default embedding model dropdown includes the new model.

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
| 2 | Click "+" → select "Embedding Model" | Control responds; expected next state is shown. |
| 3 | Fill in required fields: | Field accepts the input and displays the entered value. |
| 4 | Display Name: "Autotest Embedding Model" | Action completes without error and produces the expected UI state. |
| 5 | Name: "text-embedding-3-small" | Action completes without error and produces the expected UI state. |
| 6 | Credentials: select an existing credential | Action completes without error and produces the expected UI state. |
| 7 | Click Save | Control responds; expected next state is shown. |
| 8 | Verify the new model card appears in the Embedding Models section | Condition holds as described. |
| 9 | Verify the Default embedding model dropdown includes the new model | Condition holds as described. |

---

## Expected Final State

Verify the Default embedding model dropdown includes the new model.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create a new Embedding Model configuration.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
