---
id: ELITEA-3472
title: "Overview Tab KPI Cards Display"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3472: Overview Tab KPI Cards Display

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify all KPI metric cards on the Analytics Overview tab display correct values and formatting.

## Preconditions

- Logged into {{base_url}}
- User has project with AI activity (LLM calls, tool runs, chat messages)
- Navigate to Settings → Analytics

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Analytics → Overview tab. | Overview tab loads with 8 KPI cards visible. |
| 2 | Verify TEAM card displays "X of Y" format. | Shows active members count vs total team members. |
| 3 | Verify AI ACTIVE card shows count + percentage. | Displays AI active users count with adoption percentage (e.g., "3 +21.4%"). |
| 4 | Verify LLM CALLS card shows integer count. | Shows total LLM calls (event_type = llm). |
| 5 | Verify TOOL RUNS card shows integer count. | Shows total tool executions (event_type = tool). |
| 6 | Verify CHAT MSG card shows user messages count. | Shows user messages sent through chat interfaces. |
| 7 | Verify AGENT & PIPELINE RUNS card shows count. | Shows agents and pipelines interactions total. |
| 8 | Verify TOKENS card shows formatted count (K suffix). | Shows total LLM tokens consumed (e.g., "34.4K"). |
| 9 | Verify COST card shows USD with 4+ decimal places. | Shows estimated USD cost (e.g., "$0.0087"). |

## Pass/Fail Criteria

**Pass:** All 8 KPI cards display with correct labels, values, and formatting.
**Fail:** Any card missing, shows incorrect data, or wrong format.
