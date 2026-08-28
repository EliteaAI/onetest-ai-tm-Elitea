---
id: ELITEA-2328
title: "Hovering over Most Popular Tools bar chart shows tool name and call count"
priority: medium
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_bar_chart_tooltip.TestAnalyticsBarChartTooltip.test_bar_chart_hover_tooltip
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1957"
---

# ELITEA-2328: Hovering over Most Popular Tools bar chart shows tool name and call count

**Module:** settings-analytics · **Priority:** medium · **Type:** functional

**Objective:** Verify that Hovering over Most Popular Tools bar chart shows tool name and call count. Success is confirmed when move to a different bar — verify the tooltip updates accordingly.

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
| 1 | Navigate to Settings → Analytics → Tools tab | Target page/section loads successfully. |
| 2 | Hover over any bar in the Most Popular Tools bar chart | Action completes without error and produces the expected UI state. |
| 3 | Verify a tooltip appears showing the tool name and its usage/call count | Condition holds as described. |
| 4 | Move to a different bar — verify the tooltip updates accordingly | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Move to a different bar — verify the tooltip updates accordingly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Hovering over Most Popular Tools bar chart shows tool name and call count.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
