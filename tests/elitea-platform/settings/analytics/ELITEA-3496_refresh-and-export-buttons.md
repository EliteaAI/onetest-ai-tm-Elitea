---
id: ELITEA-3496
title: "Analytics Refresh and Export Buttons"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3496: Analytics Refresh and Export Buttons

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify refresh and export functionality works correctly.

## Preconditions

- Logged into {{base_url}}
- Navigate to Settings → Analytics

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate refresh button (circular arrows icon). | Refresh icon visible in top-right area. |
| 2 | Click refresh button. | Data reloads, loading indicators may appear briefly. |
| 3 | Verify data is current after refresh. | Any new activity since page load now visible. |
| 4 | Locate export/download button (download icon). | Export icon visible near refresh button. |
| 5 | Click export button. | Export dialog or file download initiates. |
| 6 | Verify export format. | CSV or Excel file downloads with Analytics data. |
| 7 | Open exported file. | Data matches what's displayed on Analytics page. |

## Pass/Fail Criteria

**Pass:** Refresh updates data, export downloads file with correct data.
**Fail:** Refresh does nothing, export fails, or data mismatch in export.
