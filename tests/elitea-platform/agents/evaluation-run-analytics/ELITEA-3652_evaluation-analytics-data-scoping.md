---
id: ELITEA-3652
title: "Evaluation Analytics Data Scoping Isolation"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:backend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3652: Evaluation Analytics Data Scoping Isolation

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that evaluation analytics data is scoped strictly to the selected evaluation run, isolating concurrent evaluation runs and excluding chat/agent runs.

## Preconditions

- Logged into {{base_url}}
- Agent with multiple completed evaluation runs exists
- At least two evaluation runs executed at similar times (concurrent or sequential)

## Test Data

- Evaluation Run A: Suite "Regression", completed at time T1
- Evaluation Run B: Suite "Smoke", completed at time T2 (close to T1)
- Normal agent chat run at time T3 (also close to T1)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Results History for the Agent. | Multiple evaluation runs visible. |
| 2 | Open Analytics for Evaluation Run A (Suite "Regression"). | Analytics page opens. |
| 3 | Review Costs tab data. | Data shows costs only from Run A. |
| 4 | Review Tokens tab data. | Token counts from Run A only. |
| 5 | Review Tools tab data. | Tool calls from Run A only. |
| 6 | Review Health tab data. | Event counts from Run A only. |
| 7 | Navigate back, open Analytics for Evaluation Run B. | Analytics page for Run B opens. |
| 8 | Verify data is different from Run A (assuming different suites/inputs). | Metrics differ appropriately. |
| 9 | Verify no cross-contamination between evaluation runs. | Run A and Run B have isolated data. |
| 10 | Verify normal chat runs are NOT included in evaluation analytics. | Only evaluation-triggered activity counted. |

## Pass/Fail Criteria

**Pass:** Each evaluation run's analytics shows only its own data with no cross-contamination.
**Fail:** Data from other runs appears, or chat activity leaks into evaluation analytics.
