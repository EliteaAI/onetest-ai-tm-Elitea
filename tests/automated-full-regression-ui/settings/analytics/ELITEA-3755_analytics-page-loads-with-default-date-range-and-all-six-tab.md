---
id: ELITEA-3755
title: "Analytics page loads with default date range and all six tabs visible"
priority: high
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_default_load.TestAnalyticsDefaultLoad.test_analytics_page_default_load
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1187
---

# ELITEA-3755: Analytics page loads with default date range and all six tabs visible

> **Automated.** Test: `automation/tests/ui/admin/test_analytics_default_load.py` ·
> AFS: `test-specs/settings-analytics/l2_analytics-page-default-load_ELITEA-3755.md` ·
> PR: https://github.com/EliteaAI/elitea-testing-public/pull/1187
>
> **Case-text drift found during automation** (steps 3–6): live product shows **7 tabs**
> (adds "Costs"; "Agents" is "Agents & Pipelines") and defaults to **"Last 24h" / 1-day
> range**, not the "six tabs" / "Last 24d" / "Last 7d" this case describes. The automated
> test asserts the live contract; case text needs updating. Clarification filed:
> https://github.com/EliteaAI/elitea-testing-public/issues/1185

**Module:** settings-analytics · **Priority:** high · **Type:** functional

**Objective:** Verify that Analytics page loads with default date range and all six tabs visible. Success is confirmed when verify the page does not remain in a permanent loading state.

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
| 1 | Navigate to Settings → Analytics | Target page/section loads successfully. |
| 2 | Verify the page header shows "Analytics" and the current project name badge | Condition holds as described. |
| 3 | Verify the date filter bar shows four preset buttons: Last 24h, Last 7d, Last 30d, Last 90d | Condition holds as described. |
| 4 | Verify "Last 24d" is active/highlighted by default | Condition holds as described. |
| 5 | Verify the From and To date/time pickers are present and reflect the Last 7d range | Condition holds as described. |
| 6 | Verify the following six tabs are visible: Overview, Agents, Tools, Users, Health, Guide | Condition holds as described. |
| 7 | Verify Overview tab is active and underlined by default | Condition holds as described. |
| 8 | Verify the page does not remain in a permanent loading state | Condition holds as described. |

---

## Expected Final State

Verify the page does not remain in a permanent loading state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Analytics page loads with default date range and all six tabs visible.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
