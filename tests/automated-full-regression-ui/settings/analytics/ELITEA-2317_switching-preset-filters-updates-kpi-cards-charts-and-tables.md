---
id: ELITEA-2317
title: "Switching preset filters updates KPI cards, charts, and tables on Overview tab"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_date_filter_content_refresh.TestAnalyticsOverviewContentRefresh.test_preset_switch_updates_overview_content
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1958"
---

# ELITEA-2317: Switching preset filters updates KPI cards, charts, and tables on Overview tab

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Switching preset filters updates KPI cards, charts, and tables on Overview tab. Success is confirmed when verify the top 5 ai adopters table and model usage breakdown table update.

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
| 1 | Navigate to Settings → Analytics → Overview tab under Last 7d | Target page/section loads successfully. |
| 2 | Note the values of all 6 KPI cards and the Daily Activity chart shape | Action completes without error and produces the expected UI state. |
| 3 | Click "Last 30d" | Control responds; expected next state is shown. |
| 4 | Verify KPI card values update | Condition holds as described. |
| 5 | Verify the Daily Activity chart time axis extends to cover 30 days | Condition holds as described. |
| 6 | Verify the Top 5 AI Adopters table and Model Usage Breakdown table update | Condition holds as described. |

---

## Expected Final State

Verify the Top 5 AI Adopters table and Model Usage Breakdown table update.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Switching preset filters updates KPI cards, charts, and tables on Overview tab.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
