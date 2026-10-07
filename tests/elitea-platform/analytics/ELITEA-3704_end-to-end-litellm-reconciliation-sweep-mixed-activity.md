---
id: ELITEA-3704
title: "Verify Analytics Overview Totals Reconcile With LiteLLM Across Mixed Chat/Agent/Pipeline Activity"
priority: critical
type: integration
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6705, EliteaAI/elitea_issues#6574]
---

# ELITEA-3704: Verify Analytics Overview Totals Reconcile With LiteLLM Across Mixed Chat/Agent/Pipeline Activity

**Module:** Analytics · **Priority:** Critical · **Type:** Integration

**Objective:** Verify Analytics Overview totals reconcile with LiteLLM for a fixed window containing a realistic mix of chat, agent, and pipeline activity.

**Coverage:**
- Total Cost and Total Tokens reconcile with LiteLLM across all three execution types in one window

## Preconditions

- Admin/owner access to Analytics > Overview and matching LiteLLM logs for the same window
- Ability to execute a direct chat message, a single-level agent run, and a pipeline run, all against platform-managed shared models

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "What is 2+2?" |
| Agent | Any simple existing single-level agent |
| Pipeline | Any simple existing pipeline |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Within one time window, send the test chat message (bare LLM participant) | Response received |
| 2 | Execute the test agent once | Execution completes |
| 3 | Execute the test pipeline once | Execution completes |
| 4 | Open LiteLLM logs for that window and sum total tokens and total cost across all three activities' log entries | LiteLLM totals recorded |
| 5 | Open Settings > Analytics > Overview for the identical From/To window | Total Cost and Total Tokens recorded |
| 6 | Compare the two totals | Any delta is explainable only by the UI's own "estimated from local model-price table" disclaimer tolerance, not by missing/duplicated/misattributed records |

## Expected Final State

Analytics Overview Total Cost and Total Tokens for the window reconcile with the LiteLLM-derived totals across all three activity types within the documented estimation tolerance.

## Pass/Fail Criteria

**Pass:**
- Analytics and LiteLLM totals match within the UI's documented estimation tolerance

**Fail:**
- Totals diverge beyond that tolerance, or any one activity's calls are missing/duplicated in Analytics
