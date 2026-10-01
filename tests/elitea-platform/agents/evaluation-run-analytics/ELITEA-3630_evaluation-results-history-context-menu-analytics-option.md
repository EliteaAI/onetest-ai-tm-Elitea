---
id: ELITEA-3630
title: "Evaluation Results History Context Menu Analytics Option"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3630: Evaluation Results History Context Menu Analytics Option

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that "Analytics" option appears in Agent Evaluation Results History context menu.

## Preconditions

- Logged into {{base_url}}
- Private or Team project selected
- Agent with at least one completed evaluation run exists
- Navigate to Agent → Evaluation tab

## Test Data

- Agent with completed evaluation suite runs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an Agent that has completed evaluations. | Agent detail page opens. |
| 2 | Navigate to "Evaluation" tab. | Evaluation tab content loads. |
| 3 | Locate "Results History" section or navigate to it. | Results History with past evaluation runs visible. |
| 4 | Right-click on any evaluation run row (or click three-dot menu). | Context menu appears. |
| 5 | Verify "Analytics" option is present in context menu. | "Analytics" option visible in menu. |

## Pass/Fail Criteria

**Pass:** "Analytics" option visible in Evaluation Results History context menu.
**Fail:** "Analytics" option missing from context menu.
