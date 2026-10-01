---
id: ELITEA-3651
title: "Evaluation Analytics Navigation and Page Structure"
priority: critical
type: functional
module: evaluation-run-analytics
status: draft
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3651: Evaluation Analytics Navigation and Page Structure

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Regression

**Objective:** Verify complete navigation flow to Evaluation Analytics and validate page structure (breadcrumb, header, tabs).

## Preconditions

- Logged into {{base_url}}
- Private or Team project selected
- Agent with completed evaluation suite runs exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents and open an Agent with evaluations. | Agent detail page opens. |
| 2 | Click "Evaluation" tab. | Evaluation tab content loads. |
| 3 | Open Results History section. | Past evaluation runs visible. |
| 4 | Right-click on an evaluation run row. | Context menu appears with "Analytics" option. |
| 5 | Click "Analytics". | Evaluation Analytics page opens. |
| 6 | Verify breadcrumb format. | Shows: `Agents / [Agent Name] / Evaluation / [Suite Name] / Analytics` |
| 7 | Verify header format. | Shows: "Run: [date] · Suite: [suite_name] · Version: [version]" |
| 8 | Verify exactly 4 tabs present in order. | Costs, Tokens, Tools, Health tabs visible. |
| 9 | Verify Costs tab is active by default. | Costs tab highlighted, content displayed. |
| 10 | Click each breadcrumb segment. | Each navigates to correct page. |

## Pass/Fail Criteria

**Pass:** Analytics accessible via context menu, breadcrumb/header correct, 4 tabs in order with Costs default.
**Fail:** Navigation fails, wrong structure, missing tabs, or incorrect defaults.
