---
id: ELITEA-3646
title: "Evaluation Analytics Four Tabs in Correct Order"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3646: Evaluation Analytics Four Tabs in Correct Order

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Evaluation Analytics displays exactly 4 tabs in the specified order with Costs as default.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics for any evaluation run. | Analytics page loads. |
| 2 | Locate the tab bar. | Tab bar visible below header. |
| 3 | Count the number of tabs. | Exactly 4 tabs present. |
| 4 | Verify first tab is "Costs". | First tab labeled "Costs". |
| 5 | Verify second tab is "Tokens". | Second tab labeled "Tokens". |
| 6 | Verify third tab is "Tools". | Third tab labeled "Tools". |
| 7 | Verify fourth tab is "Health". | Fourth tab labeled "Health". |
| 8 | Verify Costs tab is active by default. | Costs tab highlighted, content displayed. |
| 9 | Verify no additional tabs. | No Overview, Users, Activity, Guide tabs. |

## Pass/Fail Criteria

**Pass:** Exactly 4 tabs in order: Costs (default), Tokens, Tools, Health.
**Fail:** Wrong number of tabs, wrong order, or wrong default.
