---
id: ELITEA-3657
title: "Evaluation Analytics Not Available in Public Project"
priority: high
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, nfr:security, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3657: Evaluation Analytics Not Available in Public Project

**Module:** Evaluation Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that evaluation analytics is NOT accessible in Public project context (cost data is sensitive).

## Preconditions

- Logged into {{base_url}}
- Access to a Public project (if any exist)
- Agent with completed evaluations in Public project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Switch to Public project context. | Public project selected. |
| 2 | Navigate to Agents and open an Agent with evaluations. | Agent detail page opens. |
| 3 | Go to Evaluation tab. | Evaluation tab content loads. |
| 4 | Open Results History. | Results History visible with past runs. |
| 5 | Right-click on an evaluation run. | Context menu appears. |
| 6 | Verify "Analytics" option is NOT present. | Analytics option hidden or disabled. |
| 7 | If Analytics option somehow visible, click it. | Should not open analytics or should show access denied. |

## Pass/Fail Criteria

**Pass:** Evaluation Analytics option hidden or inaccessible in Public projects.
**Fail:** Analytics accessible in Public project, exposing potentially sensitive cost data.
