---
id: ELITEA-3499
title: "Cost Rounding 6-Decimal Precision"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3499: Cost Rounding 6-Decimal Precision

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify all cost values display with maximum 6 decimal places, rounded on 7th digit.

## Preconditions

- Logged into {{base_url}}
- Project has cost data with various precision levels
- Navigate to Settings → Analytics

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Analytics → Overview tab. | Note COST card value. |
| 2 | Count decimal places in COST. | Maximum 6 digits after decimal (e.g., "$0.008742"). |
| 3 | Open Analytics → Costs tab. | Review all cost cards. |
| 4 | Check TOTAL COST precision. | ≤6 decimal places. |
| 5 | Check INPUT TOKEN COST precision. | ≤6 decimal places (may show "< $0.00001" format). |
| 6 | Check OUTPUT TOKEN COST precision. | ≤6 decimal places. |
| 7 | Check Cost by User table values. | All cost columns ≤6 decimals. |
| 8 | Check Cost by Model table values. | All cost columns ≤6 decimals. |
| 9 | Verify no cost shows 7+ decimals. | No values like "$0.0087421". |
| 10 | Verify avg_cost_per_call if shown. | Same 6-decimal rule applies. |

## Pass/Fail Criteria

**Pass:** All cost values display with ≤6 decimal places consistently.
**Fail:** Any cost value shows more than 6 decimal places.
