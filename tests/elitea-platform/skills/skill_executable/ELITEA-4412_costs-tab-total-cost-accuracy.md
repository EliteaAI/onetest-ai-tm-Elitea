---
id: ELITEA-4412
title: "Verify Costs tab displays accurate total cost"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, costs, data-accuracy]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page
- Run has cost data in usage_event table
- Backend analytics endpoints are operational

## Test Data

| Field | Value |
|-------|-------|
| Default Tab | Costs (should open by default) |
| Cost Format | USD: `$X.XXXX` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill run analytics page | Page loads |
| 2 | Observe that "Costs" tab is selected by default | Costs tab active, data visible |
| 3 | Locate "TOTAL COST" card at top of page | Card displays total cost value |
| 4 | Note the total cost value (e.g., "$0.0167") | Value shown in format: `$X.XXXX` |
| 5 | Observe individual cost cards: INPUT TOKEN COST, OUTPUT TOKEN COST, CACHE READ COST, CACHE WRITE COST | All four cost cards visible |
| 6 | Calculate sum: Input + Output + Cache Read + Cache Write | Manual calculation of displayed values |
| 7 | Compare calculated sum with TOTAL COST | Calculated sum equals TOTAL COST |
| 8 | (Backend verification) Query usage_event table for this run_id | Backend data matches UI totals |

## Expected Final State

Costs tab displays:
- TOTAL COST = sum of all cost components
- Formula: TOTAL = Input Token Cost + Output Token Cost + Cache Read Cost + Cache Write Cost
- Values formatted as USD: `$X.XXXX`
- Data reconciles with usage_event table

## Pass/Fail Criteria

**Pass:**
- Costs tab opens by default
- TOTAL COST card displays accurate sum
- Calculation: TOTAL = Input + Output + Cache Read + Cache Write
- Values match usage_event table sum for this run_id
- No rounding errors or discrepancies

**Fail:**
- Costs tab not default
- TOTAL COST incorrect or missing
- Sum does not match component costs
- Data does not reconcile with usage_event table
- Rounding errors present
