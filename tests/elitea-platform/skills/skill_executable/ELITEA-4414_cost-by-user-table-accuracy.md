---
id: ELITEA-4414
title: "Verify Cost by User table displays accurate per-user breakdown"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, costs, tables]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page - Costs tab
- Run has user-attributed cost data
- Multiple users participated in the run (if applicable)

## Test Data

| Field | Value |
|-------|-------|
| Table Columns | USER, TOTAL COST ↓, INPUT TOKEN COST, OUTPUT TOKEN COST, CACHE READ COST, CACHE WRITE COST, SHARE |
| Sort Order | By TOTAL COST descending |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On Costs tab, scroll down to "Cost by User" table | Table is visible below cost cards |
| 2 | Observe table headers | Headers: USER, TOTAL COST ↓, INPUT TOKEN COST, OUTPUT TOKEN COST, CACHE READ COST, CACHE WRITE COST, SHARE |
| 3 | Verify each user row displays email/username | User identifier displayed (e.g., "mariam_hakobyan@epam.com") |
| 4 | Verify TOTAL COST per user | Each user's total cost shown |
| 5 | Verify cost breakdown per user | INPUT, OUTPUT, CACHE READ, CACHE WRITE costs shown per user |
| 6 | Calculate: per-user costs sum to their total | User TOTAL = Input + Output + Cache Read + Cache Write |
| 7 | Verify SHARE percentage column | SHARE % displayed for each user |
| 8 | Calculate: SHARE % = (user_cost / total_run_cost) * 100 | Percentage accurately calculated |
| 9 | Sum all user SHARE percentages | Total of all SHARE percentages = 100% |
| 10 | Verify sort order by TOTAL COST descending (↓) | Users sorted highest cost to lowest |

## Expected Final State

Cost by User table displays:
- All users who participated in the run
- Accurate per-user cost breakdown
- TOTAL COST per user = sum of their token costs
- SHARE % = (user_cost / total_run_cost) * 100
- All user SHARE percentages sum to 100%
- Sorted by TOTAL COST descending

## Pass/Fail Criteria

**Pass:**
- Table displays all participating users
- Each user's costs accurately broken down
- Per-user totals match sum of components
- SHARE % calculated correctly
- All SHARE percentages sum to 100%
- Table sorted by TOTAL COST descending

**Fail:**
- Missing users
- Incorrect cost values
- Per-user totals don't match components
- SHARE % calculation wrong
- SHARE percentages don't sum to 100%
- Sort order incorrect
