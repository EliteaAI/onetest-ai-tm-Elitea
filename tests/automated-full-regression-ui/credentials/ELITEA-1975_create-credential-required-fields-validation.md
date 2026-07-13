---
id: ELITEA-1975
title: "Create Credential — Required Fields Validation"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:toolkits]
requirements: []
---

# ELITEA-1975: Create Credential — Required Fields Validation

**Module:** toolkits-credentials · **Priority:** medium · **Type:** functional

**Objective:** Verify that the credential creation form enforces required field validation by keeping the Save button disabled until all required fields are filled, and re-disabling it if a required field is cleared.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and the Credentials section is accessible.
- A credential type with at least two required fields is selected.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the credential creation form | Form opens with all fields empty |
| 2 | Leave all fields empty | Save button remains disabled |
| 3 | Fill in only the Display Name field | Save button remains disabled |
| 4 | Fill in the other required field(s) for the selected type | Save button becomes enabled |
| 5 | Clear the Display Name field | Save button becomes disabled again |

---

## Expected Final State

The Save button is only enabled when all required fields contain valid input; removing a required value disables it again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Save button correctly reflects required field state: disabled when any required field is empty, enabled when all are filled.

**Fail:**
- Any step produces an error or unexpected result.
- Save button is enabled with empty required fields, or does not re-disable when a required field is cleared.
