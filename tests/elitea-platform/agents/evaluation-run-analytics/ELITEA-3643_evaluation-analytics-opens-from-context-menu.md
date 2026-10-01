---
id: ELITEA-3643
title: "Evaluation Analytics Opens from Context Menu"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3643: Evaluation Analytics Opens from Context Menu

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify clicking "Analytics" in Evaluation Results History opens Analytics page with evaluation-specific data.

## Preconditions

- Logged into {{base_url}}
- Private or Team project selected
- Agent with completed evaluation runs exists
- Evaluation Results History is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Results History for an Agent. | Results History displays past evaluation runs. |
| 2 | Right-click on a specific evaluation run (note suite name, date). | Context menu appears. |
| 3 | Click "Analytics" option. | Evaluation Analytics page opens. |
| 4 | Verify page loads without errors. | Analytics page displays with data. |
| 5 | Verify data corresponds to selected evaluation run. | Data is evaluation-scoped (not project-wide or agent-wide). |

## Pass/Fail Criteria

**Pass:** Evaluation Analytics page opens with evaluation-specific data.
**Fail:** Page fails to open, shows error, or displays wrong scope data.
