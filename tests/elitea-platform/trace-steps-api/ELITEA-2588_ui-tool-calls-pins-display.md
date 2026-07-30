---
id: ELITEA-2588
title: "UI displays tool call pins correctly from new paginated source"
priority: critical
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [eng:frontend, epic:5724]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5728]
---
# ELITEA-2588: UI displays tool call pins correctly from new paginated source

**Module:** Trace Steps API · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the UI correctly renders tool call pins from the new paginated trace steps endpoint for new conversations.

**Coverage:**
- Tool calls display as pins in the conversation
- Tool name is visible on the pin
- Tool inputs are visible when expanded
- Tool outputs are visible when expanded
- Timing information is displayed (if applicable)

## Preconditions

- Logged in to {{base_url}}
- Access to an agent with tools configured
- Migration to message_trace_step is deployed

## Test Data

| Field | Value |
|-------|-------|
| Agent | Agent with multiple tools |
| Tools | Various tools that return different output types |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new conversation with tool-enabled agent | Conversation is created |
| 2 | Send a message that triggers tool execution | Agent executes tools |
| 3 | Observe the tool calls displayed as pins in the response | Pins are visible for each tool call |
| 4 | Verify each pin shows the tool name | Tool name is displayed on the pin |
| 5 | Click to expand a tool call pin | Pin expands to show details |
| 6 | Verify tool inputs are displayed | Input parameters are visible and correct |
| 7 | Verify tool output is displayed | Output/result is visible |
| 8 | Check for any error indicators (if tool had an error) | Error state is correctly indicated |
| 9 | Verify pin styling matches the expected design | Pins look consistent with UI design |

## Expected Final State

All tool calls are displayed as expandable pins with correct tool name, inputs, and outputs visible.

## Pass/Fail Criteria

**Pass:**
- All tool calls appear as pins
- Tool name, inputs, outputs correctly displayed
- Pins are expandable/collapsible
- Error states indicated correctly

**Fail:**
- Missing tool call pins
- Wrong or missing tool information
- Pins don't expand or show wrong data
