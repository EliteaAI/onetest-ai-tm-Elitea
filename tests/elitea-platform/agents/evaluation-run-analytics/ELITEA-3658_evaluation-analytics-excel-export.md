---
id: ELITEA-3658
title: "Evaluation Analytics Excel Export Functionality"
priority: high
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3658: Evaluation Analytics Excel Export Functionality

**Module:** Evaluation Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that evaluation analytics data can be exported to Excel format.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open with data

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics for an evaluation run with data. | Analytics page loads with populated data. |
| 2 | Locate Export or Download button. | Export option visible (icon or button). |
| 3 | Click Export/Download. | Export dialog or direct download triggered. |
| 4 | Select Excel format if options shown. | Excel/XLSX format selected. |
| 5 | Download completes. | File downloads successfully. |
| 6 | Open the downloaded file. | File opens in Excel or compatible application. |
| 7 | Verify file contains analytics data. | Data matches what was displayed on screen. |
| 8 | Verify file includes data from all tabs. | Costs, Tokens, Tools, Health data present. |

## Pass/Fail Criteria

**Pass:** Excel file downloads with accurate analytics data from all tabs.
**Fail:** Export fails, file corrupted, or data incomplete/inaccurate.
