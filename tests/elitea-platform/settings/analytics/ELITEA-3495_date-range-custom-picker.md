---
id: ELITEA-3495
title: "Analytics Custom Date Range Picker"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3495: Analytics Custom Date Range Picker

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify custom date range picker allows selecting specific date ranges.

## Preconditions

- Logged into {{base_url}}
- Navigate to Settings → Analytics

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate From and To date pickers. | Date inputs visible with calendar icons (e.g., "From: 30/09/2026 00:..." "To: 30/09/2026 23:59"). |
| 2 | Click on "From" date picker. | Calendar popup opens. |
| 3 | Select a date 14 days ago. | Date selected, picker closes. |
| 4 | Click on "To" date picker. | Calendar popup opens. |
| 5 | Select today's date. | Date selected, picker closes. |
| 6 | Verify data refreshes for custom range. | Charts and tables update to show 14-day range. |
| 7 | Try selecting future "To" date. | Should be disabled or show validation error. |
| 8 | Try selecting "From" after "To". | Should be prevented or auto-correct. |

## Pass/Fail Criteria

**Pass:** Custom dates work, data updates, invalid ranges prevented.
**Fail:** Calendar not opening, data not refreshing, or invalid dates accepted.
