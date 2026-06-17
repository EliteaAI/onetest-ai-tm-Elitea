---
id: ELITEA-0066
title: "Smart Tool Selection behavior with embedded subagent/subpipeline"
priority: critical
type: functional
module: agents
status: ready
execution_type: manual
tags: [feat:smart-tools, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4961]
---
# ELITEA-0066: Smart Tool Selection behavior with embedded subagent/subpipeline

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** When Smart Tool Selection is enabled on Agent/Chat with attached subagents/subpipelines and toolkits: verify toolkit tools are selected differently (shown by `get_tool_schema` in Thoughts). 
Bug #4961 was that this behavior was silently lost when subagents existed.

## Preconditions

1. Available: 1 subagent, 4 toolkits
2. Smart Tool Selection toggle available on Agent and Chat pages

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent page and create or edit a test agent. Attach exactly 1 subagent, 1 subpipeline, and 4 toolkits. | All attachments are accepted and visible in agent configuration without validation errors. |
| 2 | Enable Smart Tool Selection for the agent and save configuration. | Smart Tool Selection internal tool is enabled and persists after save/reload. |
| 3 | From Agent Run, execute a prompt that can invoke attached tools/applications. Observe tool-selection behavior during/after Agent Run. | **`get_tool_schema` chips in Thoughts** = smart selection working |
| 4 | Open Chat page and create/select a chat context with attached applications: 1 subagent, 1 subpipeline, and several toolkits. | Attached applications/toolkits are successfully applied and visible in chat participant/tool context. |
| 5 | Enable Smart Tool Selection in Chat context and send a prompt requiring tool usage. | Smart Tool Selection remains active (not silently disabled) - **`get_tool_schema` chips in Thoughts** = smart selection working |

## Expected Final State

Smart Tool Selection remains active (not silently disabled) - **`get_tool_schema` chips in Thoughts** = smart selection working

## Pass/Fail Criteria

PASS: `get_tool_schema` chips appear in both Agent Run (step 3) and Chat Run (step 6); toggle on/off works consistently
FAIL:  No `get_tool_schema` chips in step 3 or 6 (bug #4961 regressed); OR inconsistent behavior between Agent and Chat; OR toggles don't persist
