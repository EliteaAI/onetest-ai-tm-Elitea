---
id: ELITEA-3477
title: "Costs Tab Daily Cost Trend Chart"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3477: Costs Tab Daily Cost Trend Chart

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Daily Cost Trend chart renders correctly showing cost distribution over time.

## Preconditions

- Logged into {{base_url}}
- Project has cost data across multiple days
- Navigate to Settings → Analytics → Costs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate "Daily Cost Trend" chart section. | Bar chart visible with title "Daily Cost Trend". |
| 2 | Verify X-axis shows dates. | Date labels correspond to selected date range. |
| 3 | Verify Y-axis shows cost values in USD. | Scale starts at $0.00 with appropriate increments. |
| 4 | Verify bars display for days with costs. | Teal/cyan colored bars for each day with activity. |
| 5 | Hover over a bar. | Tooltip shows date and exact cost value. |
| 6 | Verify days with no cost show no bar. | Empty space for days without cost data. |

## Pass/Fail Criteria

**Pass:** Chart displays cost bars for active days, tooltips work, axes labeled correctly.
**Fail:** Chart not rendering, bars missing for days with data, or tooltips not functional.
