---
id: ELITEA-2303
title: "Assign multiple roles to a user via Edit roles dialog"
priority: medium
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2303: Assign multiple roles to a user via Edit roles dialog

**Module:** settings-users-and-roles · **Priority:** medium · **Type:** functional

**Objective:** Verify that Assign multiple roles to a user via Edit roles dialog. Success is confirmed when reload the page — verify multi-role assignment persists.

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
| 2 | Click the Edit (pencil) icon on any user | Control responds; expected next state is shown. |
| 3 | Select two roles from the Roles dropdown (e.g., "editor" and "admin") | Control responds; expected next state is shown. |
| 4 | Verify both roles appear as chips in the Roles field | Condition holds as described. |
| 5 | Confirm the change | Operation completes successfully; state updates and confirmation is shown. |
| 6 | Verify the user's Role column shows both assigned roles | Condition holds as described. |
| 7 | Reload the page — verify multi-role assignment persists | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Reload the page — verify multi-role assignment persists.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Assign multiple roles to a user via Edit roles dialog.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
