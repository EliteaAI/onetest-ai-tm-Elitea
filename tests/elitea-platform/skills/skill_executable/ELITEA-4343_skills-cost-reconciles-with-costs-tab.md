---
id: ELITEA-4343
title: "Verify total skill cost reconciles with Costs tab for the same date range"
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
- Multiple skills have been executed with non-zero cost
- Analytics data available for selected date range

## Test Data

| Field | Value |
|-------|-------|
| Date Range | Last 30 days |
| Analytics Skills URL | `{{base_url}}/settings/analytics?tab=skills` |
| Analytics Costs URL | `{{base_url}}/settings/analytics?tab=costs` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Analytics → Skills tab | Skills analytics page loads |
| 2 | Set date range to "Last 30 days" | Date range updated to Last 30 days |
| 3 | Locate the "SKILL RUN COST" summary card at the top | Summary card displays total skill run cost (e.g., $5.4321) |
| 4 | Record the total "SKILL RUN COST" value | Value recorded: $5.4321 |
| 5 | Scroll to Skill Activity table and verify individual skill costs sum correctly | Sum of all skill costs in table ≈ summary card value (accounting for pagination) |
| 6 | Export Skills data to Excel (if available) and sum all skill costs | Excel total skill cost = $5.4321 |
| 7 | Navigate to Settings → Analytics → Costs tab | Costs analytics page loads |
| 8 | Ensure the same date range (Last 30 days) is selected | Date range matches "Last 30 days" |
| 9 | Identify total project cost displayed (e.g., in summary card or chart) | Total project cost displayed (e.g., $12.7890) |
| 10 | Verify skill cost is a subset of total project cost | Skill cost ($5.4321) ≤ Total project cost ($12.7890) |
| 11 | Calculate non-skill cost: Total - Skill cost = $12.7890 - $5.4321 = $7.3569 | Non-skill cost calculated (agents, direct chat, tools, etc.) |
| 12 | Verify Skills cost breakdown matches detail in Costs tab (if Costs tab shows breakdown by entity type) | Skill-related cost in Costs tab matches Skills tab total |

## Expected Final State

- Skills tab "SKILL RUN COST" reconciles with Costs tab for the same date range
- Skill cost is a subset of total project cost (skills are part of overall project cost)
- No discrepancies between Skills and Costs tabs
- Excel export matches UI totals

## Pass/Fail Criteria

**Pass:**
- Skills tab "SKILL RUN COST" = sum of all individual skill costs
- Skills cost ≤ Total project cost (Costs tab)
- Skills cost matches any skill-specific breakdown in Costs tab
- Excel export totals match UI summary card
- Reconciliation confirmed: no missing or extra cost

**Fail:**
- Skills tab "SKILL RUN COST" ≠ sum of individual skill costs
- Skills cost > Total project cost (impossible scenario)
- Discrepancy between Skills and Costs tabs for same date range
- Excel export totals ≠ UI summary card
