---
id: ELITEA-4399
title: "Empty-state message and date-range filter refresh behave consistently across all four new tables"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, empty-state, date-range]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4399: Empty-state message and date-range filter refresh behave consistently across all four new tables

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting an Agent/Pipeline and date range with no run activity shows the exact specified empty-state message for the four new tables (not a broken/empty table or stuck loading spinner), and that changing the Analytics date range refreshes Versions, Models, Trigger Sources, Recent Runs, and the KPI cards consistently with no stale data left in any single table.

**Coverage:**
- Exact empty-state copy for the new tables when no data exists in the selected range
- No broken table or indefinitely-stuck loading spinner on empty data
- Changing date range updates all four new tables and KPI cards consistently
- No table left showing stale data from the previous range while others update

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline where a date range with zero run activity can be selected (e.g. a far-future or far-past range)
- The same or another Agent/Pipeline with run data spanning more than one date-range window, to test refresh behavior

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Expected empty-state text | "No data is available for this Agent or Pipeline in the selected date range." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select an Agent/Pipeline and set the Analytics date range to a window with no run activity | Page loads without error |
| 2 | Inspect each of the four new tables (Versions, Models, Trigger Sources, Recent Runs) | Each displays the exact message "No data is available for this Agent or Pipeline in the selected date range." — not a blank table, broken layout, or indefinitely-spinning loader |
| 3 | Load the detail view for an Agent/Pipeline with run data, using the default date range; note values in all four new tables and the KPI cards | Values recorded for comparison |
| 4 | Change the date range to a narrower or different window that includes different run activity | All four new tables and the KPI cards refresh |
| 5 | Compare the refreshed values across all four tables and KPI cards | All update consistently to reflect the new range; no table shows values from the previous range while others have updated |

## Expected Final State

Empty-state messaging is shown verbatim and consistently across all four new tables when no data exists for the selected range, and changing the date range refreshes every new table and the KPI cards in sync with no stale data.

## Pass/Fail Criteria

**Pass:**
- Empty-state text matches the spec exactly across all four new tables
- No broken UI or stuck loading state on empty data
- All four tables and KPI cards update consistently after a date-range change, with no stale data left behind

**Fail:**
- Empty-state wording differs from spec, or any table shows a broken/blank state instead of the message
- Any table fails to refresh after a date-range change, or shows values inconsistent with the newly selected range
