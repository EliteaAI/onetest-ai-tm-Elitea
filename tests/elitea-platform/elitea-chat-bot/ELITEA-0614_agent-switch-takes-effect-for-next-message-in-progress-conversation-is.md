---
id: ELITEA-0614
title: "Agent switch takes effect for next message — in-progress conversation is not disrupted"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [mid-conversation, agent-switch, story:4776, r-2.0.3]
requirements: [4776]
---
# ELITEA-0614: Agent switch takes effect for next message — in-progress conversation is not disrupted

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the behavior when an admin switches the active agent while a user has an active conversation. The user's current message should complete with the previous agent (or current request), and the new agent should handle subsequent messages. The conversation should not error out or display broken state.

## Preconditions

Support Assistant enabled. Two agents configured (Agent-A and Agent-B).
Agent-A is currently active.

## Test Data

Message sent before switch: "Tell me about ELITEA features."
Message sent after switch: "Tell me more about integrations."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As regular user, send message: "Tell me about ELITEA features." | Response received from Agent-A |
| 2 | While the session is still open, Admin switches active agent to Agent-B and saves | Admin config saved |
| 3 | As regular user (same open session), send message: "Tell me more about integrations." | A valid response is received; no error shown in the chat |
| 4 | Verify the second response reflects Agent-B's behavior (or the new agent) | Response received without errors |

## Expected Final State

Response received without errors

## Pass/Fail Criteria

PASS: Both messages receive responses; no error; second response from new agent.
FAIL: Error shown after agent switch; conversation frozen; second message produces a system error.
