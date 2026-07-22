---
id: ELITEA-2299
title: "Batch delete multiple users using checkboxes"
priority: high
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2299: Batch delete multiple users using checkboxes

**Module:** settings-users-and-roles · **Priority:** high · **Type:** functional

**Objective:** Verify that Batch delete multiple users using checkboxes. Success is confirmed when verify all other users remain unaffected.

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
| 1 | Navigate to Settings → Users as Admin | Target page/section loads successfully. |
| 2 | Select checkboxes on two or more user rows | Control responds; expected next state is shown. |
| 3 | Verify the Delete (trash) icon in the header becomes active | Condition holds as described. |
| 4 | Click the header Delete icon | Control responds; expected next state is shown. |
| 5 | Verify a confirmation dialog appears | Condition holds as described. |
| 6 | Confirm deletion | Operation completes successfully; state updates and confirmation is shown. |
| 7 | Verify only the selected users are removed | Condition holds as described. |
| 8 | Verify all other users remain unaffected | Condition holds as described. |

---

## Expected Final State

Verify all other users remain unaffected.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Batch delete multiple users using checkboxes.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
