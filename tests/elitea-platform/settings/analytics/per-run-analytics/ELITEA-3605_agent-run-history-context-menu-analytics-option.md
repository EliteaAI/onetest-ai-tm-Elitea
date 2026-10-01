---
id: ELITEA-3605
title: "Agent Run History Context Menu Analytics Option"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:agents, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3605: Agent Run History Context Menu Analytics Option

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that "Analytics" option appears in Agent Run History context menu after "Restore chat" option.

## Preconditions

- Logged into {{base_url}}
- An Agent with at least one prior execution exists
- Navigate to Agents page

## Test Data

- Agent with known prior runs (e.g., runs from previous day)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an Agent that has prior executions. | Agent detail page opens with chat area. |
| 2 | Click the history/clock icon button in the chat panel. | Run History panel opens. |
| 3 | Right-click on any run row (or click three-dot menu). | Context menu appears. |
| 4 | Verify "Analytics" option is present in context menu. | "Analytics" option visible in menu. |
| 5 | Verify "Analytics" position in menu. | "Analytics" appears after "Restore chat" option. |

## Pass/Fail Criteria

**Pass:** "Analytics" option visible in context menu, positioned after "Restore chat".
**Fail:** "Analytics" option missing or incorrectly positioned.
