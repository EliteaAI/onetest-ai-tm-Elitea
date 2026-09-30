---
id: ELITEA-3473
title: "Overview Daily Activity Chart"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3473: Overview Daily Activity Chart

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Daily Activity chart renders correctly with all data series.

## Preconditions

- Logged into {{base_url}}
- Project has activity data for selected date range
- Navigate to Settings → Analytics → Overview

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate the Daily Activity chart section. | Chart area is visible with title "Daily Activity". |
| 2 | Verify chart legend shows all 4 series. | Legend displays: LLM Calls, Tool Runs, Agent & Pipeline Runs, Active Users. |
| 3 | Verify each series has distinct color. | Blue for LLM Calls, red for Tool Runs, green for Agent runs, purple for Active Users. |
| 4 | Hover over data points on the chart. | Tooltip shows date and values for each series. |
| 5 | Verify X-axis shows date range. | X-axis labels match selected date filter (e.g., 09-29 to 09-30). |
| 6 | Verify Y-axis shows numeric scale. | Y-axis has proper scale with gridlines. |

## Pass/Fail Criteria

**Pass:** Chart renders with all 4 series, proper colors, interactive tooltips, and correct axes.
**Fail:** Chart missing, series not displayed, or tooltips not working.
