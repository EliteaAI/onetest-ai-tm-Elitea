---
id: ELITEA-2329
title: "Hovering over user detail Daily Activity chart shows per-series values"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_user_detail_view.TestAnalyticsUserDetailView.test_users_tab_row_click_opens_detail_view
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1957"
---

# ELITEA-2329: Hovering over user detail Daily Activity chart shows per-series values

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Hovering over user detail Daily Activity chart shows per-series values. Success is confirmed when move to a different data point — verify the tooltip updates.

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
| 1 | Navigate to Settings → Analytics → Users tab → click a user row | Target page/section loads successfully. |
| 2 | Hover over a data point on the user's Daily Activity multi-series area chart | Action completes without error and produces the expected UI state. |
| 3 | Verify a tooltip appears showing the date and values for each event type series | Condition holds as described. |
| 4 | Move to a different data point — verify the tooltip updates | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Move to a different data point — verify the tooltip updates.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Hovering over user detail Daily Activity chart shows per-series values.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
