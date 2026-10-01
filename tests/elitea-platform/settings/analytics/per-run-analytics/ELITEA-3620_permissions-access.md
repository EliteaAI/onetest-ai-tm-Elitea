---
id: ELITEA-3620
title: "Permissions - Role-Based Access"
priority: high
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, nfr:security, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3620: Permissions - Role-Based Access

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify users with Viewer and Editor roles can access Per-Run Analytics.

## Preconditions

- Users with Viewer and Editor roles in a project
- Project has Agents/Pipelines with run history

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as user with Viewer role. | Login successful. |
| 2 | Navigate to an Agent with prior runs. | Agent page loads. |
| 3 | Open Run History and right-click on a run. | Context menu appears with "Analytics" option. |
| 4 | Click "Analytics" option. | Per-Run Analytics page opens. |
| 5 | Verify all tabs and data are visible. | Full analytics data displayed. |
| 6 | Log out and log in as user with Editor role. | Login successful. |
| 7 | Repeat steps 2-5. | Same access and functionality. |
| 8 | Verify Export functionality works for Editor. | Export downloads successfully. |

## Pass/Fail Criteria

**Pass:** Both Viewer and Editor can access Per-Run Analytics and view all data.
**Fail:** Access denied or functionality restricted for any role.
