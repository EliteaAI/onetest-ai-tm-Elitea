---
id: ELITEA-2272
title: "Project Context character limit is enforced at 2500 characters"
priority: high
type: functional
module: settings-project-params
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2272: Project Context character limit is enforced at 2500 characters

**Module:** settings-project-params · **Priority:** high · **Type:** functional

**Objective:** Verify that Project Context character limit is enforced at 2500 characters. Success is confirmed when verify the save button remains enabled at the 2500 character boundary.

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
| 1 | Navigate to Settings → Project Context | Target page/section loads successfully. |
| 2 | Enter exactly 2500 characters in the Project Background editor | Field accepts the input and displays the entered value. |
| 3 | Verify the Save button is enabled at exactly 2500 characters (regression #5667) | Condition holds as described. |
| 4 | Attempt to type additional characters beyond 2500 | Action completes without error and produces the expected UI state. |
| 5 | Verify additional characters are rejected or a character limit warning is shown | Condition holds as described. |
| 6 | Verify the Save button remains enabled at the 2500 character boundary | Condition holds as described. |

---

## Expected Final State

Verify the Save button remains enabled at the 2500 character boundary.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Project Context character limit is enforced at 2500 characters.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
