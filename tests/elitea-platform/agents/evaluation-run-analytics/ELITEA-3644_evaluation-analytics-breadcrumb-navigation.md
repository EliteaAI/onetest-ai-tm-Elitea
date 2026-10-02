---
id: ELITEA-3644
title: "Evaluation Analytics Breadcrumb Navigation"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, nfr:usability, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3644: Evaluation Analytics Breadcrumb Navigation

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify breadcrumb shows correct path and each segment navigates correctly.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open for an Agent evaluation run

## Test Data

- Agent "Test Agent" with evaluation suite "Regression Suite"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics for an evaluation run. | Analytics page loads. |
| 2 | Verify breadcrumb is displayed at top of page. | Breadcrumb visible. |
| 3 | Verify breadcrumb format. | Shows: `Agents / [Agent Name] / Evaluation / [Suite Name] / Analytics` |
| 4 | Click "Agents" segment in breadcrumb. | Navigates to Agents list page. |
| 5 | Navigate back to Analytics page. | Analytics page loads again. |
| 6 | Click "[Agent Name]" segment in breadcrumb. | Navigates to Agent detail page. |
| 7 | Navigate back to Analytics page. | Analytics page loads again. |
| 8 | Click "Evaluation" segment in breadcrumb. | Navigates to Agent's Evaluation tab. |
| 9 | Click "[Suite Name]" segment in breadcrumb. | Navigates to suite results or Results History. |

## Pass/Fail Criteria

**Pass:** Breadcrumb displays correct format with Suite name, all segments navigate correctly.
**Fail:** Breadcrumb missing, incorrect format, Suite name missing, or navigation fails.
