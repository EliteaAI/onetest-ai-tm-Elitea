---
id: ELITEA-3634
title: "Analytics — Agent Execution Run Counting"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, agent-pipeline, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6572]
---
# ELITEA-3634: Analytics — Agent Execution Run Counting

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Agent executions are counted accurately in the Analytics dashboard.

**Coverage:**
- AGENT & PIPELINE RUNS KPI increments per execution
- Agent & Pipeline Activity table tracks individual agent runs
- Tokens and costs are attributed to the agent

## Preconditions

- Logged in to {{base_url}}
- At least one Agent is configured and ready to execute
- User has access to Settings > Analytics > Agents & Pipelines tab

## Test Data

| Field | Value |
|-------|-------|
| Agent Name | Support Request Analyzer (base) |
| Test Input | "I cannot login to my account" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Analytics > Overview tab | Note AGENT & PIPELINE RUNS KPI value (e.g., N) |
| 2 | Navigate to Settings > Analytics > Agents & Pipelines tab | Note current RUNS count for the test agent |
| 3 | Navigate to Agents. Select the test agent | Agent details page opens |
| 4 | Execute the agent with test input | Agent processes and returns response |
| 5 | Navigate to Analytics > Overview tab | AGENT & PIPELINE RUNS = N + 1 |
| 6 | Navigate to Analytics > Agents & Pipelines tab | Test agent shows RUNS incremented by 1 |
| 7 | Verify agent row shows: TOTAL COST, TOTAL TOKENS, AVG LATENCY | All metrics are populated and reasonable |
| 8 | Check INPUT TOKENS, OUTPUT TOKENS columns | Token breakdown is displayed |
| 9 | Check ERRORS column | ERRORS = 0 for successful execution |

## Expected Final State

Agent execution is tracked. RUNS count incremented. Associated tokens, costs, and latency are recorded for the agent.

## Pass/Fail Criteria

**Pass:**
- AGENT & PIPELINE RUNS KPI increments by 1
- Agent's RUNS count in table increments by 1
- Tokens/costs are attributed to the agent
- Latency is recorded

**Fail:**
- Run not counted
- Metrics not attributed to the agent
- Missing latency data
