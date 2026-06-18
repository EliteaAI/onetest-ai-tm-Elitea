---
id: ELITEA-1010
title: "Verify Tool Execution Remains Paused Until User Responds"
priority: critical
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1010: Verify Tool Execution Remains Paused Until User Responds

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after the authorization dialog appears, the tool execution stays paused indefinitely without timing out immediately — and that authorizing after a wait still works correctly.

## Preconditions

- Authorization dialog is currently displayed in the agent chat

## Test Data

- Wait time: at least 30 seconds without clicking either button

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger a sensitive tool and observe the authorization dialog appearing. | Dialog is visible. Agent execution is paused. |
| 2 | Wait 30 seconds without clicking Authorize or Block. | Dialog remains visible. No auto-timeout error occurs. Agent remains paused waiting for input. |
| 3 | After 30 seconds, click [Authorize]. | Dialog closes. Tool executes. Agent completes response normally. |

## Expected Final State

Dialog closes. Tool executes. Agent completes response normally.

## Pass/Fail Criteria

Pass:
- Dialog remains displayed for at least 30 seconds without timing out
- After a wait, clicking Authorize still successfully executes the tool

Fail:
- Dialog auto-closes or shows a timeout error within a short wait
- Tool executes automatically on timeout without user input
- Clicking Authorize after a wait fails or throws an error
