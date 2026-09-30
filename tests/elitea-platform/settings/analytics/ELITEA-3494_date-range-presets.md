---
id: ELITEA-3494
title: "Analytics Date Range Presets"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3494: Analytics Date Range Presets

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify date range preset buttons filter data correctly.

## Preconditions

- Logged into {{base_url}}
- Project has data spanning multiple time periods
- Navigate to Settings → Analytics

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify date filter buttons visible. | Today, Last 7d, Last 30d, Last 90d buttons shown. |
| 2 | Click "Today" button. | Data refreshes, From/To dates set to today. |
| 3 | Verify data shows only today's activity. | Charts and tables reflect single day. |
| 4 | Click "Last 7d" button. | From date = 7 days ago, To date = today. |
| 5 | Verify data spans 7 days. | Charts show 7-day range. |
| 6 | Click "Last 30d" button. | From date = 30 days ago, To date = today. |
| 7 | Click "Last 90d" button. | From date = 90 days ago, To date = today. |
| 8 | Verify active button is highlighted. | Selected preset shows different styling (darker/selected). |

## Pass/Fail Criteria

**Pass:** All preset buttons work, date range updates correctly, active state indicated.
**Fail:** Preset doesn't update date range, wrong dates applied, or no visual feedback.
