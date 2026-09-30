---
id: ELITEA-3481
title: "Tokens Tab Daily Token Usage Chart"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3481: Tokens Tab Daily Token Usage Chart

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Daily Token Usage chart renders correctly with proper data visualization.

## Preconditions

- Logged into {{base_url}}
- Project has token usage across multiple days
- Navigate to Settings → Analytics → Tokens

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate "Daily Token Usage" chart. | Chart visible with title and subtitle "Token usage per day". |
| 2 | Verify X-axis shows dates. | Date labels match selected date range. |
| 3 | Verify Y-axis shows token count scale. | Numeric scale starting at 0 with appropriate increments. |
| 4 | Verify bars display for days with usage. | Colored bars for each day with token consumption. |
| 5 | Hover over a bar. | Tooltip shows date and token count. |

## Pass/Fail Criteria

**Pass:** Chart displays token bars for active days with working tooltips.
**Fail:** Chart not rendering or tooltips not functional.
