---
id: ELITEA-2323
title: "Users tab search by email filters the User Activity table"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_users_activity_table.TestAnalyticsUsersActivityTable.test_users_tab_activity_table_columns_and_pagination
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1957"
---

# ELITEA-2323: Users tab search by email filters the User Activity table

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Users tab search by email filters the User Activity table. Success is confirmed when clear the search input — verify all users are shown again.

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
| 1 | Navigate to Settings → Analytics → Users tab | Target page/section loads successfully. |
| 2 | Type a partial email into the "Search by email" input | Field accepts the input and displays the entered value. |
| 3 | Verify the table filters to show only rows matching the typed email | Condition holds as described. |
| 4 | Clear the search input — verify all users are shown again | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Clear the search input — verify all users are shown again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Users tab search by email filters the User Activity table.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
