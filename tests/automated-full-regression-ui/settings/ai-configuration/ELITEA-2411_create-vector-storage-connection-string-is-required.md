---
id: ELITEA-2411
title: "Create Vector Storage — Connection String is required"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2411: Create Vector Storage — Connection String is required

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create Vector Storage — Connection String is required. Success is confirmed when verify no vector storage configuration is created.

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
| 1 | Navigate to Settings → AI Configuration → click "+" → select "Vector Storage" → PGVector | Target page/section loads successfully. |
| 2 | Fill Display Name, leave Connection String empty | Field accepts the input and displays the entered value. |
| 3 | Verify the Save button is disabled OR an inline validation error appears for Connection String | Condition holds as described. |
| 4 | Verify no vector storage configuration is created | Condition holds as described. |

---

## Expected Final State

Verify no vector storage configuration is created.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create Vector Storage — Connection String is required.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
