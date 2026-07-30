---
id: ELITEA-2592
title: "Regression: HITL resume and Continue work with trace steps"
priority: high
type: regression
module: trace-steps-api
status: ready
execution_type: manual
tags: [eng:frontend, eng:backend, epic:5724, regression]
requirements: [EliteaAI/elitea_issues#5724]
---
# ELITEA-2592: Regression: HITL resume and Continue work with trace steps

**Module:** Trace Steps API · **Priority:** High · **Type:** Regression

**Objective:** Verify that Human-in-the-Loop (HITL) resume functionality and Continue feature work correctly after the trace steps migration.

**Coverage:**
- HITL pause works
- HITL resume continues correctly
- Continue conversation works
- Previous tool calls preserved after resume/continue

## Preconditions

- Logged in to {{base_url}}
- Access to an agent configured for HITL (sensitive tool confirmation)
- Migration to message_trace_step is deployed

## Test Data

| Field | Value |
|-------|-------|
| Agent | Agent with HITL-enabled tools (sensitive operations) |
| Tool | Tool that requires user confirmation |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create conversation with HITL-enabled agent | Conversation is created |
| 2 | Send message that triggers HITL tool | Agent pauses for confirmation |
| 3 | Verify tool call is visible in paused state | Tool call pin shows pending/waiting state |
| 4 | Approve the tool execution (HITL confirm) | Tool executes and completes |
| 5 | Verify tool call updates to completed state | Pin shows completed state with output |
| 6 | Navigate away from conversation | Leave the conversation |
| 7 | Return to the conversation (Continue) | Conversation loads with full history |
| 8 | Verify all tool calls from before are still visible | No missing tool calls |
| 9 | Send another message to continue the conversation | Agent responds with context intact |
| 10 | Verify new tool calls appear alongside old ones | Both old and new tools visible |

## Expected Final State

HITL resume works correctly, Continue functionality preserves all tool call history, and new messages work seamlessly with the trace steps system.

## Pass/Fail Criteria

**Pass:**
- HITL pause and resume work correctly
- Tool calls preserved after resume
- Continue loads full history
- New messages work with existing conversation

**Fail:**
- HITL resume fails
- Tool calls lost after resume/continue
- Continue shows incomplete history
