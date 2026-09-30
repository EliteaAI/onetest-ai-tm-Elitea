---
id: ELITEA-3478
title: "Costs Tab Cost by User Table"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3478: Costs Tab Cost by User Table

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Cost by User table displays per-user cost breakdown with proper formatting.

## Preconditions

- Logged into {{base_url}}
- Project has multiple users with LLM cost activity
- Navigate to Settings → Analytics → Costs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Cost by User" section. | Table visible with user cost breakdown. |
| 2 | Verify table columns. | Columns: USER, TOTAL COST, INPUT TOKEN COST, OUTPUT TOKEN COST, CACHE READ COST, CACHE WRITE COST, SHARE. |
| 3 | Verify user emails are displayed. | Each row shows user email address. |
| 4 | Verify TOTAL COST shows 6-decimal precision. | Cost values like "$0.0087" with up to 6 decimals. |
| 5 | Verify all cost columns have values. | No empty cells in cost columns (show $0.00 if zero). |
| 6 | Verify SHARE column shows percentage. | Percentage of total cost attributed to user. |
| 7 | Verify sum of SHARE equals ~100%. | All user shares should sum to approximately 100%. |

## Pass/Fail Criteria

**Pass:** Table shows all users with complete cost breakdown, 6-decimal precision, shares sum to 100%.
**Fail:** Missing columns, incorrect precision, or share percentages don't total correctly.
