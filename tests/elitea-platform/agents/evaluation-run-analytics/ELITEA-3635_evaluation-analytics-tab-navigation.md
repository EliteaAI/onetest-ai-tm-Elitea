---
id: ELITEA-3635
title: "Evaluation Analytics Tab Navigation"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3635: Evaluation Analytics Tab Navigation

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify all tabs load correctly when clicked and switching between tabs works without errors.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics. | Page loads with Costs tab active. |
| 2 | Click on "Tokens" tab. | Tokens tab becomes active, content loads. |
| 3 | Click on "Tools" tab. | Tools tab becomes active, content loads. |
| 4 | Click on "Health" tab. | Health tab becomes active, content loads. |
| 5 | Click on "Costs" tab. | Costs tab becomes active again. |
| 6 | Rapidly switch between tabs 5+ times. | Each tab loads correctly without errors. |
| 7 | Check browser console for errors. | No JavaScript errors logged. |

## Pass/Fail Criteria

**Pass:** All tabs load correctly on repeated switches, no errors.
**Fail:** Errors appear or tabs fail to load.
