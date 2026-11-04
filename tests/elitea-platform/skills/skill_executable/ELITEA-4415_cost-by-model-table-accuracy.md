---
id: ELITEA-4415
title: "Verify Cost by Model table displays accurate per-model breakdown"
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
- Run used one or more LLM models

## Test Data

| Field | Value |
|-------|-------|
| Table Columns | MODEL, TOTAL COST ↓, INPUT TOKEN COST, OUTPUT TOKEN COST, CACHE READ COST, CACHE WRITE COST, SHARE |
| Example Models | "test1", "anthropic.claude-sonnet-5-5", "claude-haiku-5-5" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On Costs tab, scroll to "Cost by Model" table | Table visible below Cost by User table |
| 2 | Observe table structure and headers | Headers present and correctly labeled |
| 3 | Verify each model row shows model name | Model names displayed (e.g., "test1", "anthropic.claude-sonnet-5-5") |
| 4 | Verify model names match actual models used during execution | Model names accurate to run execution |
| 5 | Verify TOTAL COST per model | Each model's total cost displayed |
| 6 | Verify cost breakdown per model | INPUT, OUTPUT, CACHE READ, CACHE WRITE costs per model |
| 7 | Calculate: per-model TOTAL = sum of components | Model TOTAL = Input + Output + Cache Read + Cache Write |
| 8 | Verify SHARE percentage column | SHARE % displayed for each model |
| 9 | Calculate: SHARE % = (model_cost / total_run_cost) * 100 | Percentage accurately calculated |
| 10 | Sum all model SHARE percentages | Total of all SHARE percentages = 100% |
| 11 | Verify sort order by TOTAL COST descending (↓) | Models sorted highest cost to lowest |

## Expected Final State

Cost by Model table displays:
- All models used during the run
- Model names match execution (not current skill settings)
- Accurate per-model cost breakdown
- TOTAL COST per model = sum of that model's token costs
- SHARE % = (model_cost / total_run_cost) * 100
- All model SHARE percentages sum to 100%
- Sorted by TOTAL COST descending

## Pass/Fail Criteria

**Pass:**
- All models used in run are listed
- Model names accurate to execution
- Each model's cost breakdown correct
- Per-model totals match sum of components
- SHARE % calculated correctly
- All SHARE percentages sum to 100%
- Table sorted by TOTAL COST descending

**Fail:**
- Missing models
- Model names incorrect or show current settings
- Incorrect cost values
- Per-model totals don't match components
- SHARE % calculation wrong
- SHARE percentages don't sum to 100%
- Sort order incorrect
