---
id: ELITEA-2593
title: "No duplicate or missing pins in conversation"
priority: high
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [eng:frontend, epic:5724, regression]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5728]
---
# ELITEA-2593: No duplicate or missing pins in conversation

**Module:** Trace Steps API · **Priority:** High · **Type:** Functional

**Objective:** Verify that there are no duplicate or missing tool call pins compared to current behavior — exactly one pin per tool execution.

**Coverage:**
- Each tool call shows exactly once
- No pins are missing
- No duplicate pins appear
- Count matches actual executions

## Preconditions

- Logged in to {{base_url}}
- Access to an agent with multiple tools
- Migration to message_trace_step is deployed

## Test Data

| Field | Value |
|-------|-------|
| Agent | Agent executing 5-10 tools in one turn |
| Expected count | Matches number of tool executions |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation with multi-tool agent | Conversation is created |
| 2 | Send message that triggers 5+ tool executions | Agent executes multiple tools |
| 3 | Count visible tool call pins | Note the count |
| 4 | Open DevTools and check API response | Count tools in API response |
| 5 | Compare UI count with API count | Counts match |
| 6 | Verify no duplicate tool names with same inputs/outputs | Each pin is unique |
| 7 | Refresh the page | Conversation reloads |
| 8 | Re-count visible pins after refresh | Count unchanged |
| 9 | Navigate away and back | Conversation reloads again |
| 10 | Re-count visible pins | Count still unchanged |

## Expected Final State

The number of visible pins exactly matches the number of tool executions, with no duplicates and no missing pins across page refreshes and navigation.

## Pass/Fail Criteria

**Pass:**
- Pin count matches tool execution count
- No duplicates (same tool+inputs+outputs)
- No missing pins
- Count stable across refreshes

**Fail:**
- Duplicates appear
- Pins missing
- Count changes on refresh
- API and UI counts don't match
