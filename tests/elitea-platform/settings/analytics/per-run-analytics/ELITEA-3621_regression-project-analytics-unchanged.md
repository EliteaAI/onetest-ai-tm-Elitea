---
id: ELITEA-3621
title: "Regression - Project Analytics Unchanged"
priority: high
type: regression
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3621: Regression - Project Analytics Unchanged

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Regression

**Objective:** Verify Project Analytics (Settings → Analytics) is not affected by Per-Run Analytics implementation.

## Preconditions

- Logged into {{base_url}}
- Project with activity exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → Analytics. | Project Analytics loads. |
| 2 | Verify all 9 tabs are present. | Overview, Costs, Tokens, Agents & Pipelines, Tools, Users, Activity, Health, Guide. |
| 3 | Click through each tab. | Each tab loads with data. |
| 4 | Verify data is project-wide aggregated. | Data reflects all runs in date range, not single run. |
| 5 | Verify date range selector works. | Can change date range. |
| 6 | Verify Export functionality works. | Can export project analytics. |

## Pass/Fail Criteria

**Pass:** All 9 tabs present, project-wide aggregated data, all functionality works.
**Fail:** Tabs missing, data incorrectly scoped, or functionality broken.
