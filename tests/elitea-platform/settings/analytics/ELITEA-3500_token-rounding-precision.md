---
id: ELITEA-3500
title: "Token Aggregate Rounding 2-Decimal Precision"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3500: Token Aggregate Rounding 2-Decimal Precision

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify token aggregate/average values display with 2 decimal precision.

## Preconditions

- Logged into {{base_url}}
- Project has token usage data
- Navigate to Settings → Analytics

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Analytics → Tokens tab. | Review token cards and tables. |
| 2 | Check TOTAL TOKENS format. | Shows K/M suffix (e.g., "34.4K") - 1-2 decimals max. |
| 3 | Check INPUT TOKENS format. | Same K/M format with ≤2 decimals. |
| 4 | Check tables for token averages. | Any avg token values use ≤2 decimals. |
| 5 | Open Analytics → Agents & Pipelines tab. | Check AVG LATENCY column format. |
| 6 | Verify latency format. | Shows time with reasonable precision (e.g., "2.5s"). |
| 7 | Open Analytics → Users tab. | Review token columns. |
| 8 | Verify TOTAL TOKENS formatting in table. | Uses K suffix with ≤2 decimals. |
| 9 | Check for any >2 decimal token aggregates. | None should exist. |

## Pass/Fail Criteria

**Pass:** All token aggregates/averages display with ≤2 decimal places.
**Fail:** Token averages show more than 2 decimal places.
