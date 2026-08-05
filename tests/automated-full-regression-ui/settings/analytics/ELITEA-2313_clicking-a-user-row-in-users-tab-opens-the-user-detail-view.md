---
id: ELITEA-2313
title: "Clicking a user row in Users tab opens the user detail view"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_user_detail_view.TestAnalyticsUserDetailView.test_users_tab_row_click_opens_detail_view
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1194
---

# ELITEA-2313: Clicking a user row in Users tab opens the user detail view

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Clicking a user row in Users tab opens the user detail view. Success is confirmed when click the back arrow — verify navigation returns to the user activity table.

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
| 2 | Click on any user row in the User Activity table | Control responds; expected next state is shown. |
| 3 | Verify the view transitions to the user detail page showing the user's email as the title with a back arrow | Condition holds as described. |
| 4 | Verify six KPI cards are shown: LLM Calls, Tool Calls, Chat Msg, Agent Runs, Active Days, Errors | Condition holds as described. |
| 5 | Verify Errors card value is shown in red when greater than 0 | Condition holds as described. |
| 6 | Verify a "Daily Activity" multi-series area chart is shown with "Events by type per day" subtitle | Condition holds as described. |
| 7 | Verify three summary panels are shown at the bottom: Models Used, Tools Used, Agents Used | Condition holds as described. |
| 8 | Each panel shows a count label and a list of items with their call counts | Action completes without error and produces the expected UI state. |
| 9 | Verify hovering on an a diagram shows detailes for that point in time | Condition holds as described. |
| 10 | Click the back arrow — verify navigation returns to the User Activity table | Control responds; expected next state is shown. |

---

## Expected Final State

Click the back arrow — verify navigation returns to the User Activity table.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Clicking a user row in Users tab opens the user detail view.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
