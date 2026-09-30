---
id: ELITEA-3488
title: "Users Tab User Activity Table"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, issue:6764, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437, EliteaAI/elitea_issues#6764]
---
# ELITEA-3488: Users Tab User Activity Table

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify User Activity table displays all metrics with proper sorting.

**Coverage:** Bug #6764 - Undefined secondary sort order for equal Active Days values.

## Preconditions

- Logged into {{base_url}}
- Project has multiple users with varying activity levels
- Navigate to Settings → Analytics → Users

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click on "Users" tab. | Tab loads with User Activity table. |
| 2 | Verify subtitle shows user count. | Shows "X users" count. |
| 3 | Verify all table columns present. | USER, ACTIVE DAYS, LLM CALLS, TOOL CALLS, AGENT/PIPELINE RUNS, CHAT MSG, ERRORS, TOTAL TOKENS, INPUT TOKENS, OUTPUT TOKENS, TOTAL COST, INPUT/OUTPUT/CACHE TOKEN COSTS. |
| 4 | Verify search functionality. | Search box with "Search by email" placeholder. |
| 5 | Verify default sort order. | Users sorted by a defined criteria (e.g., Active Days desc). |
| 6 | Find users with same Active Days value. | Identify rows with identical Active Days count. |
| 7 | Verify secondary sort is applied. | Users with same Active Days have consistent ordering (e.g., by Total Cost or alphabetically). |
| 8 | Verify pagination controls. | Rows per page dropdown (20 default) and page navigation. |
| 9 | Verify system users excluded. | No system/internal user emails in the list. |

## Pass/Fail Criteria

**Pass:** All columns present, defined sort order (including tie-breaker), system users excluded.
**Fail:** Columns missing, random sort for equal values, or system users visible.
