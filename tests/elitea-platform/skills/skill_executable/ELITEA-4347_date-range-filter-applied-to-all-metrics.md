---
id: ELITEA-4347
title: "Verify date range filter updates all Skills analytics metrics and charts"
priority: critical
type: functional
module: analytics-skills
status: ready
execution_type: manual
tags: [feat:skills, feat:analytics, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6929]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Multiple skills have been executed over the past 90 days with varying frequency
- Analytics data spans at least 3 months

## Test Data

| Field | Value |
|-------|-------|
| Date Range 1 | Last 7 days |
| Date Range 2 | Last 30 days |
| Date Range 3 | Custom: 2026-08-01 to 2026-08-31 (August only) |
| Analytics URL | `{{base_url}}/settings/analytics?tab=skills` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads with default date range |
| 2 | Select "Last 7 days" from date range preset dropdown | Date range updates to Last 7 days |
| 3 | Record summary card values: Skill Runs, Skills Used, Agent & Chat Uses, Skill Run Cost | Values recorded for Last 7 days (e.g., Runs=50, Cost=$0.25) |
| 4 | Record top 3 skills displayed in Skill Activity table | Top 3 skills for Last 7 days recorded |
| 5 | Click on top skill to open detail page | Skill detail page opens |
| 6 | Record KPI values and observe trend chart (7 days of data points) | KPIs and trend chart for Last 7 days recorded |
| 7 | Return to Skills list page (browser back) | Skills list restored |
| 8 | Change date range to "Last 30 days" | Date range updates to Last 30 days |
| 9 | Verify summary cards update with different values (higher totals expected) | Summary cards show increased totals (e.g., Runs=200, Cost=$1.10) |
| 10 | Verify Skill Activity table updates with different skills or different order | Table updated, different skills or order visible |
| 11 | Click on same skill again to open detail page | Skill detail page opens |
| 12 | Verify KPI values increased and trend chart now shows 30 days of data points | KPIs higher, trend chart displays 30 data points |
| 13 | Return to Skills list and select Custom date range: 2026-08-01 to 2026-08-31 | Custom date picker opens |
| 14 | Set start date: 2026-08-01, end date: 2026-08-31, and apply | Date range updates to August 2026 only |
| 15 | Verify summary cards reflect only August data | Summary cards show August-only totals |
| 16 | Verify Skill Activity table filters to August data only | Table displays skills active in August only |
| 17 | Verify API request includes correct `date_from` and `date_to` parameters (check Network tab) | API request: `date_from=2026-08-01&date_to=2026-08-31` |

## Expected Final State

- Date range filter applied consistently to all metrics: summary cards, leaderboard, detail KPIs, trend charts, breakdowns
- Changing date range triggers new API requests with correct parameters
- Data displayed matches selected date range (no stale data)

## Pass/Fail Criteria

**Pass:**
- Summary cards update correctly for all date ranges
- Skill Activity table filters by date range
- Skill detail KPIs and trend chart update based on date range
- API requests include correct `date_from` and `date_to` parameters
- No stale or incorrect data displayed

**Fail:**
- Summary cards do not update when date range changes
- Skill Activity table shows data outside selected date range
- Skill detail page ignores date range filter
- API requests missing or incorrect date parameters
- Data inconsistency across date ranges
