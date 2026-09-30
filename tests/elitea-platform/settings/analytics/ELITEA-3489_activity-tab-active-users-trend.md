---
id: ELITEA-3489
title: "Activity Tab Active Users Trend Chart"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3489: Activity Tab Active Users Trend Chart

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Active Users Trend chart displays user activity over time with filters.

## Preconditions

- Logged into {{base_url}}
- Project has user activity across multiple days
- Navigate to Settings → Analytics → Activity

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click on "Activity" tab. | Tab loads with Active Users Trend chart. |
| 2 | Verify chart title and subtitle. | Shows "Active Users Trend" with "Distinct people active per period, against those who used AI". |
| 3 | Verify legend shows two series. | "Active Users" and "AI Active Users" in legend. |
| 4 | Verify Role filter dropdown. | Dropdown with role options available. |
| 5 | Verify Day/Week/Month toggle. | Three toggle buttons for time aggregation. |
| 6 | Click "Week" toggle. | Chart re-renders with weekly aggregation. |
| 7 | Click "Month" toggle. | Chart re-renders with monthly aggregation. |
| 8 | Hover over data points. | Tooltip shows date and user counts. |

## Pass/Fail Criteria

**Pass:** Chart displays both series, toggles work, Role filter functional.
**Fail:** Missing series, toggles not working, or tooltips broken.
