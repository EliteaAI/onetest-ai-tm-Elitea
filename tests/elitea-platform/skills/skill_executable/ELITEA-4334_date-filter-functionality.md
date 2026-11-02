---
id: ELITEA-4334
title: "Verify Date filter returns accurate results in Run History"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6927]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Skill has run history spanning multiple dates
- At least 10 runs exist across different dates

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |
| Date Range | Last 7 days, Last 30 days, Custom range |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill Run History page | Run History table displays all runs |
| 2 | Locate the date filter control | Date filter dropdown or date picker is visible |
| 3 | Select "Last 7 days" filter | Table updates to show only runs from the last 7 days |
| 4 | Verify all displayed runs are within the 7-day range | Run dates are all within the selected range |
| 5 | Change filter to "Last 30 days" | Table updates to show runs from the last 30 days |
| 6 | Verify all displayed runs are within the 30-day range | Run dates match the filter criteria |
| 7 | Select a custom date range (e.g., specific start and end dates) | Table updates to show only runs within the custom range |
| 8 | Verify custom date range filtering is accurate | Only runs matching the exact date range display |
| 9 | Clear the date filter | Table returns to showing all runs |

## Expected Final State

Date filter accurately filters run history by selected date ranges, and clearing the filter restores the full list.

## Pass/Fail Criteria

**Pass:**
- Date filter control is accessible
- Filtering by preset ranges (7 days, 30 days) works correctly
- Custom date range filtering works correctly
- All displayed runs match the selected date criteria
- Clearing the filter restores all runs

**Fail:**
- Date filter is missing or non-functional
- Runs outside the selected date range are displayed
- Filtering does not update the table
- Clear filter does not restore full list
