---
id: ELITEA-2590
title: "UI groups tool calls by child agent (parent_agent_name)"
priority: medium
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [eng:frontend, epic:5724]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5728]
---
# ELITEA-2590: UI groups tool calls by child agent (parent_agent_name)

**Module:** Trace Steps API · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that tool calls from sub-agents are correctly grouped under their parent agent in the UI.

**Coverage:**
- Tool calls from main agent grouped correctly
- Tool calls from sub-agents grouped under parent
- Nesting is visually clear
- parent_agent_name field is used correctly

## Preconditions

- Logged in to {{base_url}}
- Access to an agent that invokes sub-agents (nested agents)
- Migration to message_trace_step is deployed

## Test Data

| Field | Value |
|-------|-------|
| Agent | Multi-agent setup with sub-agents |
| Sub-agents | At least 2 different sub-agents with tools |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation with multi-agent setup | Conversation is created |
| 2 | Send message that triggers main agent and sub-agents | Multiple agents execute with tool calls |
| 3 | Observe tool calls grouping in UI | Tool calls are grouped by agent |
| 4 | Verify main agent's tool calls are separate | Main agent tools clearly identified |
| 5 | Verify each sub-agent's tool calls are grouped together | Sub-agent tools grouped under parent |
| 6 | Check visual hierarchy/nesting | Nesting is visually clear and correct |
| 7 | Expand each group to verify correct tool attribution | Tools belong to correct agent |

## Expected Final State

Tool calls are correctly grouped by their parent agent, with clear visual hierarchy showing which tools belong to which agent in a multi-agent conversation.

## Pass/Fail Criteria

**Pass:**
- Tool calls grouped by parent_agent_name
- Visual hierarchy clear
- Correct attribution of tools to agents
- Nesting preserved from execution

**Fail:**
- Tools mixed up between agents
- No grouping visible
- Wrong parent attribution
