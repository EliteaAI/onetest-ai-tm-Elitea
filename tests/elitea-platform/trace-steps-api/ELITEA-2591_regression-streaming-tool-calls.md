---
id: ELITEA-2591
title: "Regression: Streaming responses with tool calls work correctly"
priority: high
type: regression
module: trace-steps-api
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, epic:5724, regression]
requirements: [EliteaAI/elitea_issues#5724]
---
# ELITEA-2591: Regression: Streaming responses with tool calls work correctly

**Module:** Trace Steps API · **Priority:** High · **Type:** Regression

**Objective:** Verify that streaming responses continue to work correctly after the trace steps migration — tool call pins should appear in real-time as they execute.

**Coverage:**
- Tool calls appear during streaming (not only after completion)
- Pins update in real-time
- No duplicate pins after streaming completes
- Final state matches completed response

## Preconditions

- Logged in to {{base_url}}
- Access to an agent with tools that take noticeable time to execute
- Migration to message_trace_step is deployed

## Test Data

| Field | Value |
|-------|-------|
| Agent | Agent with slow tools (e.g., web search, API calls) |
| Expected behavior | Pins appear as tools start executing |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation with tool-enabled agent | Conversation is created |
| 2 | Send a message that triggers multiple tool executions | Agent starts processing |
| 3 | Observe UI during streaming response | Text streams in real-time |
| 4 | Watch for tool call pins appearing | Pins appear as tools START executing (not after) |
| 5 | Verify pins update as tools complete | Pins show completion status |
| 6 | Wait for full response to complete | Response fully rendered |
| 7 | Count the number of tool call pins | Count matches actual tool executions |
| 8 | Verify no duplicate pins | Each tool appears exactly once |

## Expected Final State

Tool call pins appear progressively during streaming, not all at once after completion. Final count matches the number of tool executions with no duplicates.

## Pass/Fail Criteria

**Pass:**
- Pins appear during streaming in real-time
- Pins update as tools complete
- No duplicates after completion
- Final state is consistent

**Fail:**
- Pins only appear after full response
- Duplicate pins appear
- Pins missing or inconsistent with execution
