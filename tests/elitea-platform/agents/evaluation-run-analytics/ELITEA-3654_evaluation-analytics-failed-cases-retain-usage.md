---
id: ELITEA-3654
title: "Evaluation Analytics Failed Cases Retain Usage Data"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:backend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3654: Evaluation Analytics Failed Cases Retain Usage Data

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that failed test cases within an evaluation run still contribute their resource usage to analytics.

## Preconditions

- Logged into {{base_url}}
- Evaluation suite with test cases that can fail (e.g., assertion failure, timeout, model error)
- At least one evaluation run with mixed pass/fail results

## Test Data

- Evaluation run with:
  - 3 passed test cases
  - 2 failed test cases (due to assertion failure or error)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Run evaluation with known failure scenarios. | Evaluation completes with some failures. |
| 2 | View evaluation results, confirm some cases failed. | Mix of pass/fail status visible. |
| 3 | Open Analytics from Results History. | Analytics page opens. |
| 4 | Review Costs tab TOTAL COST. | Cost is non-zero and includes failed cases' consumption. |
| 5 | Review Tokens tab. | Token count reflects all cases (passed + failed). |
| 6 | Review Health tab. | Error counts reflect failures; total count includes all runs. |
| 7 | Verify total cost is not just from passed cases. | Failed cases contribute their usage. |

## Pass/Fail Criteria

**Pass:** Analytics reflects full resource usage including failed test cases.
**Fail:** Failed cases' usage missing or zeroed out.
