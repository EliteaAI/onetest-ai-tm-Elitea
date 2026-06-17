---
id: ELITEA-0383
title: "Regression — Chat History Preserved in Agent Chat After Sub-Participant Change"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:agents, regression, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4790]
---
# ELITEA-0383: Regression — Chat History Preserved in Agent Chat After Sub-Participant Change

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Regression — verify that the parent agent's own chat history still works correctly in a Chat session after the sub-participant `chat_history` exclusion change. The agent must be able to reference previous messages in the same conversation.

**Coverage:**
- Agent correctly recalls its own prior response when asked
- Chat history is not cleared or broken by the sub-participant change
- The exclusion of `chat_history` applies only to sub-participant payloads, not to the parent conversation

## Preconditions

- Logged in to {{base_url}}
- An agent is configured (sub-agent setup is not required for this test)
- A Chat session is open with the agent
- Enhancement EliteaAI/elitea_issues#4790 is deployed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat session with the agent and send an initial message (e.g., 'Tell me a fun fact about space') | Agent responds with a fact |
| 2 | Send a follow-up message in the same chat: 'What was the fact you just told me?' | Agent correctly recalls and restates its previous response, demonstrating it has access to the current chat history. No errors or 'I don't know what you mean' responses. |

## Expected Final State

Agent correctly recalls and restates its previous response, demonstrating it has access to the current chat history. No errors or 'I don't know what you mean' responses.

## Pass/Fail Criteria

**Pass:**
- Agent correctly recalls its prior response from the same chat session

**Fail:**
- Agent cannot recall the previous message (history appears lost or empty)
- Agent returns an error or claims it has no prior context
