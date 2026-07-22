---
id: ELITEA-2340
title: "Secret name is required — Save disabled when name is empty"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2340: Secret name is required — Save disabled when name is empty

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Secret name is required — Save disabled when name is empty. Success is confirmed when verify the save button becomes enabled.

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
| 1 | Navigate to Settings → Secrets and click "+" | Target page/section loads successfully. |
| 2 | Leave the Name field empty, fill the Value field | Action completes without error and produces the expected UI state. |
| 3 | Verify the Save button is disabled or an inline validation error is shown | Condition holds as described. |
| 4 | Enter a valid name | Field accepts the input and displays the entered value. |
| 5 | Verify the Save button becomes enabled | Condition holds as described. |

---

## Expected Final State

Verify the Save button becomes enabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Secret name is required — Save disabled when name is empty.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
