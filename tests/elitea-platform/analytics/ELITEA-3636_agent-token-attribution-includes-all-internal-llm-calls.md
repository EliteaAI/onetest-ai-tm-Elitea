---
id: ELITEA-3636
title: "Analytics — Agent Token Attribution Includes All Internal LLM Calls"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, agent-pipeline, tokens, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6571]
---
# ELITEA-3636: Analytics — Agent Token Attribution Includes All Internal LLM Calls

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that all tokens consumed during an agent execution (including tool-use iterations) are attributed to that agent.

**Coverage:**
- Agent with tool use makes multiple LLM calls
- All LLM calls are aggregated under the agent's token count
- Cache tokens (if used) are included

## Preconditions

- Logged in to {{base_url}}
- Agent configured with tools that trigger multiple LLM iterations
- User has access to Analytics > Agents & Pipelines tab

## Test Data

| Field | Value |
|-------|-------|
| Agent | Agent with MCP tools enabled |
| Expected Behavior | Multiple LLM calls during tool orchestration |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Analytics > Agents & Pipelines. Note agent's current TOTAL TOKENS | Initial value recorded |
| 2 | Navigate to Analytics > Tokens. Note TOTAL TOKENS KPI | Initial total recorded |
| 3 | Execute the agent with a request requiring tool use | Agent makes multiple LLM calls (planning, tool calls, final response) |
| 4 | Navigate to Analytics > Agents & Pipelines tab | Agent's TOTAL TOKENS increased |
| 5 | Calculate: Agent token increase = New tokens - Initial tokens | Token increase noted |
| 6 | Navigate to Analytics > Tokens tab | TOTAL TOKENS KPI increased by similar amount |
| 7 | Verify agent's INPUT TOKENS and OUTPUT TOKENS | Both values populated and reasonable |
| 8 | Check CACHE READ TOKENS and CACHE WRITE TOKENS | Cache usage tracked if applicable |

## Expected Final State

All tokens from the agent's multi-turn execution are attributed to the agent. No tokens are "lost" or unattributed.

## Pass/Fail Criteria

**Pass:**
- Agent token increase ≥ sum of visible LLM interactions
- Token breakdown (input/output/cache) is populated
- Overall token KPI increase matches agent attribution

**Fail:**
- Tokens missing from agent attribution
- Significant discrepancy between agent tokens and total increase
