---
id: ELITEA-3638
title: "Evaluation Analytics Tools Tab Content"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3638: Evaluation Analytics Tools Tab Content

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Tools tab displays Tool Details table with evaluation-specific tool usage data.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open for evaluation that used tools

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics and click Tools tab. | Tools tab content displayed. |
| 2 | Verify Tool Details table is present. | Table visible with subtitle "X tools". |
| 3 | Verify TOOL column. | Tool names displayed. |
| 4 | Verify CALLS column. | Integer call counts per tool. |
| 5 | Verify USERS column. | User count per tool. |
| 6 | Verify AVG LATENCY column. | Time in "Xs" or "Yms" format. |
| 7 | Verify ERRORS column. | Integer error counts. |
| 8 | Verify tools listed are from this evaluation run only. | No tools from other runs/evaluations. |

## Pass/Fail Criteria

**Pass:** Tool Details table with 5 columns, evaluation-scoped data only.
**Fail:** Columns missing, wrong data, or data from other evaluations.
