---
id: ELITEA-3637
title: "Analytics — Agent Execution Error Tracking"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, agent-pipeline, errors, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6572]
---
# ELITEA-3637: Analytics — Agent Execution Error Tracking

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that failed agent executions are tracked in the ERRORS column while still counting the run.

**Coverage:**
- Failed agent run increments RUNS count
- Failed agent run increments ERRORS count
- Partial token/cost consumption before failure is tracked

## Preconditions

- Logged in to {{base_url}}
- Ability to trigger an agent error (e.g., invalid tool configuration, timeout)
- User has access to Analytics > Agents & Pipelines tab

## Test Data

| Field | Value |
|-------|-------|
| Error Scenario | Agent with misconfigured tool or timeout condition |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Analytics > Agents & Pipelines. Note agent's RUNS and ERRORS | Initial values recorded |
| 2 | Execute the agent in a way that causes an error | Agent execution fails with error |
| 3 | Navigate to Analytics > Agents & Pipelines tab | Agent row is visible |
| 4 | Verify RUNS column | RUNS incremented by 1 (failed run still counts) |
| 5 | Verify ERRORS column | ERRORS incremented by 1 |
| 6 | Check TOTAL TOKENS | Tokens consumed before failure are tracked |
| 7 | Check AVG LATENCY | Latency includes the failed run |

## Expected Final State

Failed execution is tracked as both a run and an error. Partial resource consumption is recorded.

## Pass/Fail Criteria

**Pass:**
- RUNS +1 for failed execution
- ERRORS +1 for failed execution
- Partial tokens/costs tracked

**Fail:**
- Failed run not counted
- ERRORS not incremented
- Partial consumption not tracked
