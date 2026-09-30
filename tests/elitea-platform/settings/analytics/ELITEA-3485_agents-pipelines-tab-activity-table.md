---
id: ELITEA-3485
title: "Agents & Pipelines Tab Activity Table"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3485: Agents & Pipelines Tab Activity Table

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify Agent & Pipeline Activity table displays complete metrics for each entity.

## Preconditions

- Logged into {{base_url}}
- Project has agent/pipeline executions
- Navigate to Settings → Analytics → Agents & Pipelines

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Agent & Pipeline Activity" section. | Table visible with activity data. |
| 2 | Verify subtitle shows entity count. | Shows "X agents & pipelines" count. |
| 3 | Verify table columns. | Columns: AGENT/PIPELINE, RUNS, USERS, TOTAL COST, INPUT/OUTPUT TOKEN COST, CACHE costs, TOTAL/INPUT/OUTPUT TOKENS, CACHE tokens, AVG LATENCY, ERRORS. |
| 4 | Verify search functionality. | Search box with placeholder "Search by agent or pipeline". |
| 5 | Enter search term. | Table filters to matching entities. |
| 6 | Verify AVG LATENCY format. | Shows time in seconds (e.g., "2.5s", "1.4s"). |
| 7 | Verify ERRORS column. | Shows error count as integer. |
| 8 | Verify pagination controls. | "Rows per page" dropdown and page navigation visible. |

## Pass/Fail Criteria

**Pass:** Table shows all metrics, search works, pagination functional.
**Fail:** Missing columns, search not filtering, or pagination broken.
