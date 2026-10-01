---
id: ELITEA-3623
title: "Export Edge Cases"
priority: high
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3623: Export Edge Cases

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify export works correctly for runs with no tool usage and runs with errors.

## Preconditions

- Logged into {{base_url}}
- Runs with varying data availability exist

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics for run with no tool usage. | Analytics page loads. |
| 2 | Verify Tools tab shows empty state. | Empty state message displayed. |
| 3 | Click Export button. | Export initiates. |
| 4 | Verify file downloads successfully. | File downloaded without error. |
| 5 | Open Excel and check Tools sheet. | Sheet present with "No data" or empty state. |
| 6 | Verify other sheets have data. | Costs, Tokens, Health sheets contain data. |
| 7 | Open Per-Run Analytics for run with errors. | Analytics page loads. |
| 8 | Note error counts in UI. | Record values. |
| 9 | Export and verify error data in Excel. | Error data matches UI values. |

## Pass/Fail Criteria

**Pass:** Export handles empty tools gracefully, error data exported correctly.
**Fail:** Export fails for edge cases, or data missing/incorrect.
