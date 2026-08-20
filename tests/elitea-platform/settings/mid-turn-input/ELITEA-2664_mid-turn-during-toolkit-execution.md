---
id: ELITEA-2664
title: "Verify mid-turn input handling when agent is executing toolkit tools"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Mid-turn Input (Beta) toggle is enabled
- Conversation has an agent with toolkit attached (e.g., web search, code execution)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Agent | Agent with toolkit (web search, GitHub, etc.) |
| Initial prompt | "Search for the latest news about AI and summarize the top 5 articles" |
| Mid-turn message | "Focus on healthcare AI applications" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send prompt that triggers multiple tool calls | Agent starts executing tools |
| 2 | While tools are being called, send mid-turn message | Message is sent |
| 3 | Observe agent behavior | Agent acknowledges input at next natural point between tool calls |
| 4 | Wait for turn to complete | Turn completes |
| 5 | Review final response | Response incorporates mid-turn guidance |

## Expected Final State

Agent handles mid-turn input appropriately between tool calls, incorporating the guidance without disrupting tool execution.

## Pass/Fail Criteria

**Pass:**
- Mid-turn input delivered between tool calls
- Agent adjusts subsequent behavior based on input
- Tool execution completes successfully

**Fail:**
- Tool execution disrupted
- Mid-turn input ignored
- Error during tool calling
