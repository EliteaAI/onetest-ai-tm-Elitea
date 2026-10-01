---
id: ELITEA-3606
title: "Pipeline Run History Context Menu Analytics Option"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:pipelines, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3606: Pipeline Run History Context Menu Analytics Option

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that "Analytics" option appears in Pipeline Run History context menu after "Restore chat" option.

## Preconditions

- Logged into {{base_url}}
- A Pipeline with at least one prior execution exists
- Navigate to Pipelines page

## Test Data

- Pipeline with known prior runs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Pipeline that has prior executions. | Pipeline detail page opens. |
| 2 | Click the history/clock icon button to open Run History. | Run History panel opens. |
| 3 | Right-click on any run row (or click three-dot menu). | Context menu appears. |
| 4 | Verify "Analytics" option is present in context menu. | "Analytics" option visible in menu. |
| 5 | Verify "Analytics" position in menu. | "Analytics" appears after "Restore chat" option (same position as Agents). |

## Pass/Fail Criteria

**Pass:** "Analytics" option visible in context menu, positioned consistently with Agent Run History.
**Fail:** "Analytics" option missing or positioned differently than Agent Run History.
