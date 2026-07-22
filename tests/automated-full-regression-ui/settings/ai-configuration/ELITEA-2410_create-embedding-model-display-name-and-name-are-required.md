---
id: ELITEA-2410
title: "Create Embedding Model — Display Name and Name are required"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2410: Create Embedding Model — Display Name and Name are required

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create Embedding Model — Display Name and Name are required. Success is confirmed when verify no model is created in either case.

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
| 1 | Navigate to Settings → AI Configuration → click "+" → select "Embedding Model" | Target page/section loads successfully. |
| 2 | Leave Display Name empty — verify Save is disabled or validation error shown | Action completes without error and produces the expected UI state. |
| 3 | Fill Display Name, leave Name empty — verify Save is disabled or validation error shown | Field accepts the input and displays the entered value. |
| 4 | Verify no model is created in either case | Condition holds as described. |

---

## Expected Final State

Verify no model is created in either case.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create Embedding Model — Display Name and Name are required.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
