---
id: ELITEA-3653
title: "Evaluation Analytics Includes LLM-as-Judge Scoring Costs"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:backend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3653: Evaluation Analytics Includes LLM-as-Judge Scoring Costs

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify evaluation analytics includes costs from LLM-as-judge scoring (when evaluation suite uses judge-based metrics like coherence, factuality).

## Preconditions

- Logged into {{base_url}}
- Evaluation suite configured with LLM-as-judge metrics (e.g., coherence, factuality)
- Evaluation run completed successfully

## Test Data

- Evaluation suite with judge-based scoring enabled
- Known approximate cost for test execution vs. judge scoring

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run an evaluation with LLM-as-judge metrics. | Evaluation completes. |
| 2 | Open Analytics from Results History for that run. | Analytics page opens. |
| 3 | Review Costs tab TOTAL COST. | Total includes both test execution and judge costs. |
| 4 | Verify total is higher than just test execution would be. | Judge scoring added to total. |
| 5 | Review Cost by Model table. | Judge model(s) appear in the table. |
| 6 | Review Tokens tab. | Token usage includes judge prompt/completion. |
| 7 | Review Usage by Model table. | Judge model shows token consumption. |

## Pass/Fail Criteria

**Pass:** LLM-as-judge costs and tokens visible and included in totals.
**Fail:** Judge costs missing from analytics.
