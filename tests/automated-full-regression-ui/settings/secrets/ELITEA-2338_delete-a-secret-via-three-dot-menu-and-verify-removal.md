---
id: ELITEA-2338
title: "Delete a secret via three-dot menu and verify removal"
priority: medium
type: functional
module: settings-secrets
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2338: Delete a secret via three-dot menu and verify removal

**Module:** settings-secrets · **Priority:** medium · **Type:** functional

**Objective:** Verify that Delete a secret via three-dot menu and verify removal. Success is confirmed when reload the page — verify the deleted secret does not reappear.

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
| 2 | Click the three-dot menu on any secret row | Control responds; expected next state is shown. |
| 3 | Verify the dropdown shows: Edit value, Hide, Delete | Condition holds as described. |
| 4 | Click "Delete" | Control responds; expected next state is shown. |
| 5 | Verify a confirmation dialog appears | Condition holds as described. |
| 6 | Confirm deletion | Operation completes successfully; state updates and confirmation is shown. |
| 7 | Verify the secret is removed from the table | Condition holds as described. |
| 8 | Reload the page — verify the deleted secret does not reappear | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Reload the page — verify the deleted secret does not reappear.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Delete a secret via three-dot menu and verify removal.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
