---
id: ELITEA-4215
title: "Verify date range selection with metric display"
priority: medium
type: ui
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:analytics, feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7272]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Skills have been used across multiple time periods (at least 7 days of data)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/settings/analytics` |
| Tab | Skills |
| Time ranges | Today, Last 7d, Last 30d, Last 90d, Custom |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → Analytics → Skills | Skills analytics page loads with default "Last 7d" selected |
| 2 | Check summary cards display values for last 7 days | SKILL RUNS, SKILLS USED, AGENT & CHAT USES, SKILL RUN COST show numeric values |
| 3 | Note the values in all 4 summary cards | Values recorded for comparison |
| 4 | Click "Last 30d" time range button | Button becomes active/selected |
| 5 | Wait for page to refresh with 30-day data | Page reloads or updates |
| 6 | Verify summary cards update with different values | SKILL RUNS, SKILLS USED, AGENT & CHAT USES, SKILL RUN COST show updated values (typically higher for longer period) |
| 7 | Verify "Most Used Skills" chart updates | Chart displays data for 30-day period |
| 8 | Verify Skill Activity table updates | Table shows skills used in last 30 days |
| 9 | Click "Last 90d" time range button | Page updates with 90-day data |
| 10 | Verify all metrics reflect 90-day period | Cards, chart, and table all show 90-day data |
| 11 | Click custom date range (if available) → Set "From" and "To" dates | Custom date picker opens |
| 12 | Select specific date range (e.g., last 14 days) | Dates selected |
| 13 | Click apply/update button | Page refreshes with custom date range data |
| 14 | Verify all metrics reflect custom date range | Cards, chart, and table show data for selected custom period |
| 15 | Check that "AGENT & CHAT USES" values update correctly across all time ranges | Values change appropriately based on selected time period |

## Expected Final State

Date range selector works correctly, and all metrics (including AGENT & CHAT USES) update accurately based on the selected time period. Summary cards, chart, and table data remain consistent with the selected date range.

## Pass/Fail Criteria

**Pass:**
- Date range selector changes active state when clicked
- All metrics update based on selected time period
- Summary cards show different values for different time ranges
- Chart and table data are consistent with selected date range
- "AGENT & CHAT USES" values update correctly
- Custom date range works if available

**Fail:**
- Date range selector doesn't respond to clicks
- Metrics don't update when time range changes
- Data inconsistency between cards, chart, and table
- "AGENT & CHAT USES" values don't update
- Page errors when changing date ranges
