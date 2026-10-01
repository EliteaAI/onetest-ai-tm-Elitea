---
id: ELITEA-3654
title: "Evaluation Analytics Project Access Control"
priority: critical
type: functional
module: evaluation-run-analytics
status: draft
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, nfr:security, issue:6817, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3654: Evaluation Analytics Project Access Control

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Regression

**Objective:** Verify Evaluation Analytics available in Private/Team projects but NOT in Public projects.

## Preconditions

- Logged into {{base_url}}
- Access to Private, Team, and Public projects (if available)
- Agents with evaluation runs in each project type

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Switch to Private project. | Private project selected. |
| 2 | Navigate to Agent → Evaluation → Results History. | Results History visible. |
| 3 | Right-click evaluation run, verify "Analytics" option present. | Analytics option visible. |
| 4 | Click Analytics, verify page opens. | Analytics page loads successfully. |
| 5 | Switch to Team project. | Team project selected. |
| 6 | Navigate to Agent → Evaluation → Results History. | Results History visible. |
| 7 | Right-click evaluation run, verify "Analytics" option present. | Analytics option visible. |
| 8 | Click Analytics, verify page opens. | Analytics page loads successfully. |
| 9 | Switch to Public project (if available). | Public project selected. |
| 10 | Navigate to Agent → Evaluation → Results History. | Results History visible. |
| 11 | Right-click evaluation run, verify "Analytics" option is hidden/disabled. | Analytics option NOT available. |

## Pass/Fail Criteria

**Pass:** Analytics available in Private/Team, hidden in Public projects.
**Fail:** Analytics missing in Private/Team OR accessible in Public project.
