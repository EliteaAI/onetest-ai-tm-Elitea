---
id: ELITEA-3491
title: "Health Tab Requests vs Errors Chart"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3491: Health Tab Requests vs Errors Chart

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Requests vs Errors chart displays trend with error overlay.

## Preconditions

- Logged into {{base_url}}
- Project has API activity with some errors
- Navigate to Settings → Analytics → Health

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click on "Health" tab. | Tab loads with Requests vs Errors chart. |
| 2 | Verify chart title and subtitle. | Shows "Requests vs Errors" with "Total requests trend with error overlay". |
| 3 | Verify two lines/areas in chart. | Teal line for requests, red for errors. |
| 4 | Verify X-axis shows date range. | Date labels match selected filter. |
| 5 | Verify Y-axis for requests (left). | Shows request count scale. |
| 6 | Verify Y-axis for errors (right). | Shows error count scale (may be different range). |
| 7 | Hover over data points. | Tooltip shows date, request count, and error count. |

## Pass/Fail Criteria

**Pass:** Chart shows both request and error trends with dual Y-axes.
**Fail:** Single series only, missing axis, or tooltips not working.
