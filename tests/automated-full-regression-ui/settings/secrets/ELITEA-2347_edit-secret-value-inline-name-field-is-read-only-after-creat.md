---
id: ELITEA-2347
title: "Edit secret value inline — name field is read-only after creation"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2347: Edit secret value inline — name field is read-only after creation

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Edit secret value inline — name field is read-only after creation. Success is confirmed when click the eye icon to reveal — verify the value matches the newly entered value.

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
| 1 | Navigate to Settings → Secrets | Target page/section loads successfully. |
| 2 | Click the three-dot menu on any secret → click "Edit value" | Control responds; expected next state is shown. |
| 3 | Verify the Value field becomes inline editable | Condition holds as described. |
| 4 | Verify the Name field is read-only (cannot be edited) | Condition holds as described. |
| 5 | Enter a new value and click the ✓ (checkmark) icon | Field accepts the input and displays the entered value. |
| 6 | Verify the secret saves without error | Condition holds as described. |
| 7 | Click the eye icon to reveal — verify the value matches the newly entered value | Control responds; expected next state is shown. |

---

## Expected Final State

Click the eye icon to reveal — verify the value matches the newly entered value.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Edit secret value inline — name field is read-only after creation.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
