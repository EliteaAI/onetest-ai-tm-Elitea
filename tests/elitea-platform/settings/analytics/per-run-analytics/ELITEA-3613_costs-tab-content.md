---
id: ELITEA-3613
title: "Costs Tab Content - Cards and Tables"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3613: Costs Tab Content - Cards and Tables

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Costs tab displays info banner, all 5 cost cards with 6-decimal precision, and Cost by User/Model tables.

## Preconditions

- Logged into {{base_url}}
- Per-Run Analytics page open on Costs tab
- Run had LLM activity with associated costs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics on Costs tab. | Costs tab content displayed. |
| 2 | Verify info banner is displayed. | Shows: "Costs are estimated from a local model-price table; actual provider invoices may differ." |
| 3 | Verify TOTAL COST card is present. | Card shows total cost (e.g., "$0.0087"). |
| 4 | Verify INPUT TOKEN COST card is present. | Card shows input token cost. |
| 5 | Verify OUTPUT TOKEN COST card is present. | Card shows output token cost. |
| 6 | Verify CACHE READ COST card is present. | Card shows cache read cost (may be "$0.00"). |
| 7 | Verify CACHE WRITE COST card is present. | Card shows cache write cost. |
| 8 | Verify all costs show max 6 decimal precision. | No cost shows more than 6 digits after decimal. |
| 9 | Scroll to Cost by User table. | Table displays user(s) with cost breakdown. |
| 10 | Scroll to Cost by Model table. | Table displays model(s) with cost breakdown. |

## Pass/Fail Criteria

**Pass:** Info banner, 5 cost cards with 6-decimal precision, and both tables present.
**Fail:** Any element missing, wrong precision, or incorrect data.
