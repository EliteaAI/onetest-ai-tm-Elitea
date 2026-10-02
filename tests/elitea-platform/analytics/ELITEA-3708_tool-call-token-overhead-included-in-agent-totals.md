---
id: ELITEA-3708
title: "Verify Toolkit/MCP Tool-Call Token Overhead Is Included in Agent Analytics Totals"
priority: high
type: integration
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6631]
---

# ELITEA-3708: Verify Toolkit/MCP Tool-Call Token Overhead Is Included in Agent Analytics Totals

**Module:** Analytics · **Priority:** High · **Type:** Integration

**Objective:** Verify tokens/cost consumed by toolkit/MCP tool-calling steps within an agent run are included in that agent's Analytics totals, not just the final-answer LLM tokens.

**Coverage:**
- Agent total includes every LLM turn, including tool-call-authoring and tool-result-processing turns

## Preconditions

- Access to Analytics > Agents & Pipelines detail view and matching LiteLLM logs
- An agent with an attached toolkit/MCP tool that it will invoke mid-run

## Test Data

| Field | Value |
|-------|-------|
| Agent | Agent with a toolkit/MCP tool it will invoke for the test input |
| Input | A prompt that requires the agent to call the attached tool |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Execute the agent with the test input, triggering ≥1 tool call mid-run | Execution completes, including the tool call |
| 2 | Open LiteLLM logs for the run and sum tokens/cost for every LLM call in the run, including the tool-call-authoring and tool-result-processing turns | Total LiteLLM tokens/cost recorded |
| 3 | Open the agent's detail view in Analytics > Agents & Pipelines for the same run | Agent's total tokens/cost recorded |
| 4 | Compare the two totals | Analytics total includes the tool-call turns' tokens/cost, matching the LiteLLM sum (not just the final-answer turn) |

## Expected Final State

The agent's Analytics total includes every LLM turn in the run, including tool-call-related turns.

## Pass/Fail Criteria

**Pass:**
- Analytics total matches the full LiteLLM sum including tool-call turns

**Fail:**
- Analytics total only reflects the final-answer turn, undercounting tool-call-related tokens/cost
