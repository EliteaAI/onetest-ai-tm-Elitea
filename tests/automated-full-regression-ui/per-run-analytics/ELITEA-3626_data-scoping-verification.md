---
id: ELITEA-3626
title: "Data Scoping Verification - Run vs Project Level"
priority: critical
type: functional
module: per-run-analytics
status: draft
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3626: Data Scoping Verification - Run vs Project Level

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Regression

**Objective:** Verify Per-Run Analytics shows run-scoped data, not project-wide data.

## Preconditions

- Logged into {{base_url}}
- Agent/Pipeline with multiple runs exists
- Project has significant activity (many runs)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → Analytics. | Project Analytics loads. |
| 2 | Note TOTAL COST value on Costs tab. | Record project_total_cost. |
| 3 | Note TOTAL TOKENS value on Tokens tab. | Record project_total_tokens. |
| 4 | Navigate to an Agent's Run History. | Run History panel opens. |
| 5 | Open Per-Run Analytics for any single run. | Analytics page loads. |
| 6 | Get Per-Run TOTAL COST value. | Record run_total_cost. |
| 7 | Assert run_total_cost < project_total_cost. | Per-Run cost is smaller. |
| 8 | Navigate to Tokens tab. | Tokens content loads. |
| 9 | Get Per-Run TOTAL TOKENS value. | Record run_total_tokens. |
| 10 | Assert run_total_tokens < project_total_tokens. | Per-Run tokens is smaller. |
| 11 | Navigate to Tools tab. | Tools content loads. |
| 12 | Note tool names listed. | Record run_tools. |
| 13 | Open Per-Run Analytics for different run with different tools. | Analytics page loads. |
| 14 | Verify tool list is different. | Each run shows only its own tools. |

## Automation Notes

- Store values in variables for comparison
- Use numeric parsing for cost/token values
- May need multiple test runs with known different tool usage

## Pass/Fail Criteria

**Pass:** Per-Run values are always subset of project values, tools are run-specific.
**Fail:** Per-Run data equals project data or shows tools from other runs.
