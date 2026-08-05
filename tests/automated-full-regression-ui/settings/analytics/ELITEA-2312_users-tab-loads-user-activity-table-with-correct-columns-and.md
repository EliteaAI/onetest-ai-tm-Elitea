---
id: ELITEA-2312
title: "Users tab loads User Activity table with correct columns and pagination"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_users_activity_table.TestAnalyticsUsersActivityTable.test_users_tab_activity_table_columns_and_pagination
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1190
---

# ELITEA-2312: Users tab loads User Activity table with correct columns and pagination

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Users tab loads User Activity table with correct columns and pagination. Success is confirmed when verify pagination controls are present: rows per page selector, page range label (e.g., "1–1 of 1"), prev/next arrows.

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
| 2 | Verify the section header shows "User Activity" and a user count (e.g., "1 users") | Condition holds as described. |
| 3 | Verify a "Search by email" input is present in the top right | Condition holds as described. |
| 4 | Verify the table has the following columns: USER, EVENTS, DAYS, LLM, TOOL, AGENT, CHAT MSG, ERRORS | Condition holds as described. |
| 5 | Verify the ERRORS column value is shown in red when greater or equal 0 | Condition holds as described. |
| 6 | Verify pagination controls are present: Rows per page selector, page range label (e.g., "1–1 of 1"), prev/next arrows | Condition holds as described. |

---

## Expected Final State

Verify pagination controls are present: Rows per page selector, page range label (e.g., "1–1 of 1"), prev/next arrows.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Users tab loads User Activity table with correct columns and pagination.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
