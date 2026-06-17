---
id: ELITEA-0615
title: "Messages are processed by the currently configured active agent"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [agent-selection, backend-driven, correct-agent, story:4776, r-2.0.3]
requirements: [4776, 4773]
---
# ELITEA-0615: Messages are processed by the currently configured active agent

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that messages sent through the Support Assistant are handled by the agent currently configured as active in Admin → Guardrails — not a random or fallback agent. This is confirmed by comparing the response style/knowledge between two different agents.

## Preconditions

Two different agents are configured in the Support Assistant project: Agent-A (e.g., general assistant) and Agent-B (e.g., a different specialized agent with distinct behavior/system prompt).
Platform Admin can switch the active agent in Admin → Guardrails.

## Test Data

Agent-A configured as active initially.
Test prompt: "Describe your purpose in one sentence." (This should produce distinct answers from each agent.)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Agent-A as the active support agent in Admin → Guardrails; save | Config saved |
| 2 | As a regular user, open Support Assistant and send: "Describe your purpose in one sentence." | Response received from Agent-A's behavior/persona |
| 3 | Note the response content | Record the response for comparison |
| 4 | As Admin, switch the active agent to Agent-B in Admin → Guardrails; save | Config saved |
| 5 | As regular user, start a NEW chat session in Support Assistant and send the same prompt | Response is received from Agent-B — response is visibly different from Agent-A's response in step 2 |

## Expected Final State

Response is received from Agent-B — response is visibly different from Agent-A's response in step 2

## Pass/Fail Criteria

PASS: Agent-A response and Agent-B response are distinctly different; switching agents changes behavior.
FAIL: Both agents produce identical responses; agent switch has no effect; old agent continues handling requests after switch.
