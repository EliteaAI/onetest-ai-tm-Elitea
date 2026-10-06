---
id: ELITEA-2399
title: "Create a new Vector Storage (PGVector) configuration"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2399: Create a new Vector Storage (PGVector) configuration

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Create a new Vector Storage (PGVector) configuration. Success is confirmed when verify the default vector storage dropdown includes the new configuration.

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
| 2 | Click "+" → select "Vector Storage" | Control responds; expected next state is shown. |
| 3 | Select provider: PGVector | Control responds; expected next state is shown. |
| 4 | Fill in required fields: | Field accepts the input and displays the entered value. |
| 5 | Display Name: "Autotest PGVector" | Action completes without error and produces the expected UI state. |
| 6 | Connection String: a valid PostgreSQL connection string | Action completes without error and produces the expected UI state. |
| 7 | Click Save | Control responds; expected next state is shown. |
| 8 | Verify the new vector storage card appears in the Vector Storage section | Condition holds as described. |
| 9 | Verify the Default vector storage dropdown includes the new configuration | Condition holds as described. |

---

## Expected Final State

Verify the Default vector storage dropdown includes the new configuration.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Create a new Vector Storage (PGVector) configuration.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
