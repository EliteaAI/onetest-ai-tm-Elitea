---
id: ELITEA-3476
title: "Costs Tab Summary Cards Display"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3476: Costs Tab Summary Cards Display

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Costs tab displays all cost metric cards with correct 6-decimal precision.

## Preconditions

- Logged into {{base_url}}
- Project has LLM activity with associated costs
- Navigate to Settings → Analytics → Costs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click on Costs tab. | Costs tab loads with info note banner and metric cards. |
| 2 | Verify info note is displayed. | Shows "Costs are estimated from a local model-price table; actual provider invoices may differ." |
| 3 | Verify TOTAL COST card. | Shows total cost with "estimated USD cost" label (e.g., "$0.0087"). |
| 4 | Verify INPUT TOKEN COST card. | Shows input token cost (e.g., "< $0.00001"). |
| 5 | Verify OUTPUT TOKEN COST card. | Shows output token cost with 4+ decimals. |
| 6 | Verify CACHE READ COST card. | Shows cache read cost (may be "$0.00" if no cache usage). |
| 7 | Verify CACHE WRITE COST card. | Shows cache write cost with proper precision. |
| 8 | Verify all costs show 6 decimal places max. | No cost value shows more than 6 digits after decimal point. |

## Pass/Fail Criteria

**Pass:** All 5 cost cards display with proper labels, values, and 6-decimal precision.
**Fail:** Cards missing, incorrect precision, or values showing more than 6 decimals.
