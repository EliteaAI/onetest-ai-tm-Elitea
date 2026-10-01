---
id: ELITEA-3636
title: "Evaluation Analytics Costs Tab Content"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3636: Evaluation Analytics Costs Tab Content

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Costs tab displays info banner, cost cards, and tables with evaluation-specific data including LLM-as-judge costs.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open on Costs tab
- Evaluation run included test execution AND LLM-as-judge scoring

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics on Costs tab. | Costs tab content displayed. |
| 2 | Verify info banner is displayed. | Shows disclaimer about estimated costs. |
| 3 | Verify TOTAL COST card is present. | Shows total cost including test execution + LLM-as-judge. |
| 4 | Verify INPUT TOKEN COST card is present. | Card shows input token cost. |
| 5 | Verify OUTPUT TOKEN COST card is present. | Card shows output token cost. |
| 6 | Verify CACHE READ COST card is present. | Card shows cache read cost. |
| 7 | Verify CACHE WRITE COST card is present. | Card shows cache write cost. |
| 8 | Verify all costs show max 6 decimal precision. | No more than 6 digits after decimal. |
| 9 | Scroll to Cost by User table. | Table displays user(s). |
| 10 | Scroll to Cost by Model table. | Table displays model(s) used in evaluation. |
| 11 | Verify costs include both test execution and LLM-as-judge. | Total reflects complete evaluation cost. |

## Pass/Fail Criteria

**Pass:** All cost cards and tables present with evaluation-scoped data including judge costs.
**Fail:** Elements missing, wrong precision, or judge costs not included.
