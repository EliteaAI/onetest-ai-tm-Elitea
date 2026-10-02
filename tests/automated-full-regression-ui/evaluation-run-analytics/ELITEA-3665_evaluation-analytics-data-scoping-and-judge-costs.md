---
id: ELITEA-3665
title: "Evaluation Analytics Data Scoping and LLM Judge Costs"
priority: critical
type: functional
module: evaluation-run-analytics
status: draft
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:backend, issue:6817, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3665: Evaluation Analytics Data Scoping and LLM Judge Costs

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Regression

**Objective:** Verify data isolation between evaluation runs, LLM-as-judge costs included, and failed cases retain usage.

## Preconditions

- Logged into {{base_url}}
- Agent with multiple completed evaluation runs (different suites or times)
- At least one evaluation with LLM-as-judge metrics (coherence, factuality)
- At least one evaluation with some failed test cases

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Analytics for Evaluation Run A. | Analytics loads for Run A. |
| 2 | Note the Total Cost and Total Tokens values. | Values recorded. |
| 3 | Navigate back and open Analytics for Evaluation Run B. | Analytics loads for Run B. |
| 4 | Verify values differ from Run A (assuming different inputs). | Data is isolated per run. |
| 5 | Open Analytics for evaluation with LLM-as-judge metrics. | Analytics loads. |
| 6 | Verify Cost by Model table shows judge model(s). | Judge model costs included in totals. |
| 7 | Open Analytics for evaluation with failed test cases. | Analytics loads. |
| 8 | Verify Total Cost is non-zero. | Failed cases still contribute usage. |
| 9 | Verify Health tab shows error counts > 0. | Failures tracked in Health tab. |

## Pass/Fail Criteria

**Pass:** Runs isolated, judge costs included, failed cases retain usage data.
**Fail:** Data leaks between runs, judge costs missing, or failed case usage zeroed.
