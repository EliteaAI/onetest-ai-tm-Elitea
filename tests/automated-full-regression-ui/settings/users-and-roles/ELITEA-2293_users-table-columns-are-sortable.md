---
id: ELITEA-2293
title: "Users table columns are sortable"
priority: high
type: functional
module: settings-users-and-roles
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_users_column_sorting.TestUsersColumnSorting.test_users_table_columns_are_sortable
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1979"
---

# ELITEA-2293: Users table columns are sortable

**Module:** settings-users-and-roles · **Priority:** high · **Type:** functional

**Objective:** Verify that Users table columns are sortable. Success is confirmed when click the last login column header — verify rows sort by last login datetime.

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
| 2 | Click the Name column header (↕) | Control responds; expected next state is shown. |
| 3 | Verify rows sort alphabetically ascending by name | Condition holds as described. |
| 4 | Click again — verify rows sort descending | Control responds; expected next state is shown. |
| 5 | Click the Email column header — verify rows sort by email | Control responds; expected next state is shown. |
| 6 | Click the Last login column header — verify rows sort by last login datetime | Control responds; expected next state is shown. |

---

## Expected Final State

Click the Last login column header — verify rows sort by last login datetime.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Users table columns are sortable.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
