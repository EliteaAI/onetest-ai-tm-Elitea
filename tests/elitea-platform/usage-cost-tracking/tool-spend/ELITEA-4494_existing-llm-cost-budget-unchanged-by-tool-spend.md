---
id: ELITEA-4494
title: "Existing LLM Cost Budget figures on Usage page remain unchanged by Tool Spend tracking"
priority: critical
type: regression
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4494: Existing LLM Cost Budget figures on Usage page remain unchanged by Tool Spend tracking

**Module:** Usage Cost Tracking · **Priority:** Critical · **Type:** Regression

**Objective:** Confirm that introducing Tool Spend tracking has not altered the existing LLM budget KPIs, progress bar, forecast, or reset date on Settings → Usage.

**Coverage:**
- LLM budget KPI cards (SPENT, FORECAST, AVG/DAY, TOKENS) unaffected by Tool Spend
- "Project usage · [Month]" block unaffected by Paid Tools activity
- "Members" section (Whole Project tab) unaffected by paid-tool usage

## Preconditions

- Logged in to `{{base_url}}`
- User has access to at least one Team project and one Personal project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/usage` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Settings → Usage for a team project. | Page loads; record SPENT, FORECAST, AVG/DAY, TOKENS KPI cards and the "Project usage · [Month]" block ($ of $, % used, reset date, forecast line, limit-source hint). |
| 2 | Repeat step 1 for a personal project. | Same KPI set recorded for the personal project. |
| 3 | Trigger several LLM-only interactions (plain chat messages, no paid tool involved) in the team project, then refresh Settings → Usage. | LLM budget numbers update only from LLM usage; values are consistent with LLM-only activity. |
| 4 | Confirm no Paid Tools activity occurred in the same window. | LLM budget numbers are unaffected by any Paid Tools activity. |
| 5 | Open the "Members" section (team project, Whole Project tab). | Member/Spent/Limit/Used% columns display exactly as before, unaffected by paid-tool usage. |

## Expected Final State

LLM Cost Budget KPIs, progress bar, forecast, and reset date on Settings → Usage remain driven only by LLM usage, with no cross-contamination from Tool Spend/Paid Tools data.

## Pass/Fail Criteria

**Pass:**
- LLM budget figures match pre-Tool-Spend baseline behavior
- Members section unaffected by paid-tool usage

**Fail:**
- LLM budget KPIs change due to paid-tool activity
- Members section reflects paid-tool spend instead of only LLM spend
