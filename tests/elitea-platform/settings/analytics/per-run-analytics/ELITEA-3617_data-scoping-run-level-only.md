---
id: ELITEA-3617
title: "Data Scoping - All Data Reflects Run Level Only"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3617: Data Scoping - All Data Reflects Run Level Only

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify all analytics data (costs, tokens, tools) is scoped to the selected run, not project-wide.

## Preconditions

- Logged into {{base_url}}
- Agent/Pipeline with multiple runs exists
- Know approximate values for single run vs project total

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Project Settings → Analytics. | Project-level analytics loads. |
| 2 | Note TOTAL COST and TOTAL TOKENS for project. | Record project totals. |
| 3 | Navigate to Agent/Pipeline Run History. | Run History panel opens. |
| 4 | Open Per-Run Analytics for a single run. | Per-Run Analytics loads. |
| 5 | Compare Per-Run TOTAL COST with Project TOTAL COST. | Per-Run cost is significantly smaller. |
| 6 | Compare Per-Run TOTAL TOKENS with Project TOTAL TOKENS. | Per-Run tokens significantly smaller. |
| 7 | Navigate to Tools tab. | Tools content displayed. |
| 8 | Verify tools list contains only tools used in this run. | No tools from other runs appear. |

## Pass/Fail Criteria

**Pass:** All per-run values are appropriately smaller than project totals.
**Fail:** Per-run data equals or exceeds project totals (not properly scoped).
