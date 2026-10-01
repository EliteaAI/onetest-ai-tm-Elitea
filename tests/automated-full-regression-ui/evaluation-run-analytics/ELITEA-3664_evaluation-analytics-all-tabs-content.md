---
id: ELITEA-3664
title: "Evaluation Analytics All Tabs Content Verification"
priority: critical
type: functional
module: evaluation-run-analytics
status: draft
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3664: Evaluation Analytics All Tabs Content Verification

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Regression

**Objective:** Verify all four tabs (Costs, Tokens, Tools, Health) display correct content and tables.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open for evaluation run with usage data

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | On Costs tab, verify info banner displayed. | Disclaimer about estimated costs visible. |
| 2 | Verify 5 cost cards: Total, Input, Output, Cache Read, Cache Write. | All cards present with $ values (max 6 decimals). |
| 3 | Scroll to Cost by User and Cost by Model tables. | Both tables visible with data. |
| 4 | Click "Tokens" tab. | Tokens tab loads. |
| 5 | Verify 5 token cards: Total, Input, Output, Cache Read, Cache Write. | All cards present with K/M suffix for large numbers. |
| 6 | Verify Usage by User and Usage by Model tables. | Both tables visible. |
| 7 | Click "Tools" tab. | Tools tab loads. |
| 8 | Verify Tool Details table with columns: Tool, Calls, Users, Avg Latency, Errors. | Table with 5 columns present. |
| 9 | Click "Health" tab. | Health tab loads. |
| 10 | Verify Event Type table with columns: Event Type, Total, Errors, Error Rate, Avg Latency. | Table with 5 columns and status indicators. |
| 11 | Rapidly switch between all tabs 3 times. | No errors, each tab loads correctly. |

## Pass/Fail Criteria

**Pass:** All tabs display correct cards, tables, and columns with proper formatting.
**Fail:** Missing elements, wrong formats, or errors on tab switching.
