---
id: ELITEA-2318
title: "Switching preset filters updates content on Agents, Tools, and Users tabs"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_date_filter_content_refresh.TestAnalyticsTabContentRefresh.test_preset_switch_updates_agents_tools_and_users_tabs
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1958"
---

# ELITEA-2318: Switching preset filters updates content on Agents, Tools, and Users tabs

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Switching preset filters updates content on Agents, Tools, and Users tabs. Success is confirmed when verify the agent activity table updates.

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
| 1 | Navigate to Settings → Analytics → Agents tab under Last 24d | Target page/section loads successfully. |
| 2 | Note the Chat Messages chart and Most Active Agents bar chart data | Action completes without error and produces the expected UI state. |
| 3 | Click "Last 30d" | Control responds; expected next state is shown. |
| 4 | Verify both charts update their data | Condition holds as described. |
| 5 | Verify the Agent Activity table updates | Condition holds as described. |
| 6 | Repeat the steps for Users and Tools tabs | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Repeat the steps for Users and Tools tabs.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Switching preset filters updates content on Agents, Tools, and Users tabs.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
