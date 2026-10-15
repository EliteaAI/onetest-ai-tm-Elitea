---
id: ELITEA-2310
title: "Analytics page loads with default date range and all ten tabs visible"
priority: high
type: functional
module: settings-analytics
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.admin.test_analytics_default_load.TestAnalyticsDefaultLoad.test_analytics_page_default_load
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/2442
---

# ELITEA-2310: Analytics page loads with default date range and all ten tabs visible

> **Automated.** Test: `automation/tests/ui/admin/test_analytics_default_load.py` ·
> AFS: `test-specs/settings-analytics/l2_analytics-page-default-load_ELITEA-2310.md` ·
> PR (round 2, current): https://github.com/EliteaAI/elitea-testing-public/pull/2442 ·
> PR (round 1, original automation): https://github.com/EliteaAI/elitea-testing-public/pull/1187
>
> **Case-text drift, round 1 (original automation, 2026-08):** live product showed 7
> tabs (adds "Costs"; "Agents" is "Agents & Pipelines") and defaulted to "Last 24h" /
> 1-day range, not the "six tabs" / "Last 24d" / "Last 7d" this case originally
> described. Clarification filed:
> https://github.com/EliteaAI/elitea-testing-public/issues/1185 (that issue has since
> been deleted upstream — found 410 Gone during this round-2 update, 2026-10-15; noted
> here rather than silently dropped, no action taken on it).
>
> **Case-text drift, round 2 (this update, 2026-10-15, issue #2440,
> `adjust-automated-test`, triage Class A — UI drift, product already shipped the
> change):** the product moved again since round 1. The default preset's label
> changed from "Last 24h" to "Today", its date math changed from a rolling 24-hour
> window to a calendar-day window (`EL-6791`, 2026-09-28), and three more tabs were
> added — "Tokens", "Skills" (visible only to users holding the Skills-list
> permission), "Activity" (`EL-6211`/`EL-6929`/`EL-5110`) — growing the tab bar from
> seven to ten. The automated test asserts the current live contract; this case text
> is updated below to match. Full evidence: AFS § Adjustment.

**Module:** settings-analytics · **Priority:** high · **Type:** functional

**Objective:** Verify that Analytics page loads with default date range and all ten tabs visible. Success is confirmed when verify the page does not remain in a permanent loading state.

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
| 3 | Verify the date filter bar shows four preset buttons: Today, Last 7d, Last 30d, Last 90d | Condition holds as described. |
| 4 | Verify "Today" is active/highlighted by default | Condition holds as described. |
| 5 | Verify the From and To date/time pickers are present and span the current calendar day (From = start of today 00:00, To = end of today 23:59) | Condition holds as described. |
| 6 | Verify the following ten tabs are visible, in order: Overview, Costs, Tokens, Agents & Pipelines, Skills, Tools, Users, Activity, Health, Guide (Skills is visible only for a user holding the Skills-list permission) | Condition holds as described. |
| 7 | Verify Overview tab is active and underlined by default | Condition holds as described. |
| 8 | Verify the page does not remain in a permanent loading state | Condition holds as described. |

---

## Expected Final State

Verify the page does not remain in a permanent loading state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Analytics page loads with default date range and all ten tabs visible.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
