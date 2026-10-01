---
id: ELITEA-3627
title: "Regression - Project Analytics Not Affected"
priority: high
type: regression
module: per-run-analytics
status: draft
execution_type: automated
tags: [feat:analytics, feat:settings, issue:6816, r-2.0.7, regression]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3627: Regression - Project Analytics Not Affected

**Module:** Per-Run Analytics · **Priority:** High · **Type:** Regression

**Objective:** Verify Project Analytics (Settings → Analytics) is unchanged after Per-Run Analytics implementation.

## Preconditions

- Logged into {{base_url}}
- Project with activity exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → Analytics. | Project Analytics loads. |
| 2 | Verify Overview tab is present and active by default. | Overview tab displayed. |
| 3 | Verify Overview has 8 KPI cards. | TEAM, AI ACTIVE, LLM CALLS, TOOL RUNS, CHAT MSG, AGENT & PIPELINE RUNS, TOKENS, COST. |
| 4 | Click Costs tab. | Costs content loads with 5 cards. |
| 5 | Click Tokens tab. | Tokens content loads with 5 cards. |
| 6 | Click Agents & Pipelines tab. | Activity table loads. |
| 7 | Click Tools tab. | Tools content loads. |
| 8 | Click Users tab. | Users activity table loads. |
| 9 | Click Activity tab. | Activity charts load. |
| 10 | Click Health tab. | Health metrics load. |
| 11 | Click Guide tab. | Documentation content loads. |
| 12 | Verify date range selector works. | Can select different ranges. |
| 13 | Verify Export button works. | Export downloads project data. |

## Automation Notes

- This is a smoke test for Project Analytics
- Verify each tab loads without errors (not deep content validation)
- Compare against baseline if available

## Pass/Fail Criteria

**Pass:** All 9 tabs load, core functionality works.
**Fail:** Any tab missing, broken, or functionality changed.
