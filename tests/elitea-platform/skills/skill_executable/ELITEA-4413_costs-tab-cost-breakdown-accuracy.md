---
id: ELITEA-4413
title: "Verify Costs tab shows accurate cost breakdown by component"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, costs, data-accuracy]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page - Costs tab
- Run has cost data for various components (input, output, cache)

## Test Data

| Field | Value |
|-------|-------|
| Cost Components | INPUT TOKEN COST, OUTPUT TOKEN COST, CACHE READ COST, CACHE WRITE COST |
| Format | USD: `$X.XXXX` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On Costs tab, observe all cost metric cards | Four cost cards visible |
| 2 | Verify "INPUT TOKEN COST" card value | Displays cost for input tokens consumed (e.g., "$0.0002") |
| 3 | Verify "OUTPUT TOKEN COST" card value | Displays cost for output tokens generated (e.g., "$0.0165") |
| 4 | Verify "CACHE READ COST" card value | Displays cost for cache hits (may be "$0.00") |
| 5 | Verify "CACHE WRITE COST" card value | Displays cost for cache writes (may be "$0.00") |
| 6 | Calculate: Input + Output + Cache Read + Cache Write | Sum of all four components |
| 7 | Compare sum with TOTAL COST card | Sum equals TOTAL COST |
| 8 | (Backend) Cross-reference with usage_event data | Individual costs match DB values |

## Expected Final State

Cost breakdown displays:
- INPUT TOKEN COST: accurate value for input tokens
- OUTPUT TOKEN COST: accurate value for output tokens
- CACHE READ COST: accurate value for cache reads (may be $0.00)
- CACHE WRITE COST: accurate value for cache writes (may be $0.00)
- Sum of all four = TOTAL COST
- All values in USD format: `$X.XXXX`

## Pass/Fail Criteria

**Pass:**
- All four cost cards display values
- Each cost card shows accurate individual cost
- INPUT + OUTPUT + CACHE READ + CACHE WRITE = TOTAL COST
- Values match usage_event table
- All formatted as `$X.XXXX`

**Fail:**
- Missing cost cards
- Incorrect cost values
- Sum does not equal TOTAL COST
- Data does not match usage_event table
- Format incorrect
