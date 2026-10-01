---
id: ELITEA-3644
title: "Evaluation Analytics Available in Team Project"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3644: Evaluation Analytics Available in Team Project

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify evaluation analytics feature is accessible in Team project context.

## Preconditions

- Logged into {{base_url}}
- Access to a Team project
- Agent with completed evaluations in Team project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Switch to Team project context. | Team project selected. |
| 2 | Navigate to Agents and open an Agent with evaluations. | Agent detail page opens. |
| 3 | Go to Evaluation tab. | Evaluation tab content loads. |
| 4 | Open Results History. | Results History visible with past runs. |
| 5 | Right-click on an evaluation run. | Context menu appears. |
| 6 | Verify "Analytics" option is present. | Analytics option visible. |
| 7 | Click "Analytics". | Analytics page opens with full functionality. |

## Pass/Fail Criteria

**Pass:** Evaluation Analytics fully accessible and functional in Team project.
**Fail:** Analytics option missing or disabled in Team project.
