---
id: ELITEA-3618
title: "Excel Export Functionality"
priority: high
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3618: Excel Export Functionality

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Export button works and downloads Excel file with all 4 tabs matching UI data.

## Preconditions

- Logged into {{base_url}}
- Per-Run Analytics page open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics for any run. | Analytics page loads. |
| 2 | Locate Export/Download button in header. | Button visible. |
| 3 | Note values displayed in UI (costs, tokens, etc.). | Record key values for comparison. |
| 4 | Click Export button. | File download initiates. |
| 5 | Verify file extension. | File is .xlsx format. |
| 6 | Open file in Excel. | File opens without errors. |
| 7 | Verify Costs sheet present with data. | Costs data matches UI. |
| 8 | Verify Tokens sheet present with data. | Tokens data matches UI. |
| 9 | Verify Tools sheet present with data. | Tools data matches UI. |
| 10 | Verify Health sheet present with data. | Health data matches UI. |

## Pass/Fail Criteria

**Pass:** Export downloads .xlsx with 4 sheets, data matches UI display.
**Fail:** Export fails, wrong format, sheets missing, or data mismatch.
