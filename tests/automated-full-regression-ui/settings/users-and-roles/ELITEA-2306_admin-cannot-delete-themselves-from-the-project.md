---
id: ELITEA-2306
title: "Admin cannot delete themselves from the project"
priority: high
type: functional
module: settings-users-and-roles
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2306: Admin cannot delete themselves from the project

**Module:** settings-users-and-roles · **Priority:** high · **Type:** functional

**Objective:** Verify that Admin cannot delete themselves from the project. Success is confirmed when verify the admin remains in the table.

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
| 1 | Log in as Admin role | User is authenticated and lands on the expected landing page. |
| 2 | Navigate to Settings → Users | Target page/section loads successfully. |
| 3 | Locate your own user row | Action completes without error and produces the expected UI state. |
| 4 | Verify the Delete icon is disabled OR a confirmation error appears when attempting self-deletion | Condition holds as described. |
| 5 | Verify the Admin remains in the table | Condition holds as described. |

---

## Expected Final State

Verify the Admin remains in the table.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Admin cannot delete themselves from the project.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
