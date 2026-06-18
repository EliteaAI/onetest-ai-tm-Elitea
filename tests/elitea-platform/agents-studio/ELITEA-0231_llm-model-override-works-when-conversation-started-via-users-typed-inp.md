---
id: ELITEA-0231
title: "LLM Model Override Works When Conversation Started via User's Typed Input"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0231: LLM Model Override Works When Conversation Started via User's Typed Input

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the LLM model override is fully functional when the conversation is initiated by the user typing their own message.

**Coverage:**
- Model override applied to sessions started via user's free-text input
- No override-restriction error on user-initiated conversations

## Preconditions

- Published agent is open in chat (agentId=16)
- Default model is "Anthropic Claude 4.5 Sonnet"

## Test Data

Override model: GPT-4.1
User message: "Tell me about ELITEA agents"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open published agent in chat. | Chat input is ready. |
| 2 | Switch model to GPT-4.1 via the model selector. | Toolbar shows GPT-4.1. |
| 3 | Type 'Tell me about ELITEA agents' in the chat input and press Send. | Message is sent. |
| 4 | Observe the response. | Agent returns a valid response without any error messages. |

## Expected Final State

Agent returns a valid response without any error messages.

## Pass/Fail Criteria

**Pass:**
- Response is generated successfully with the overridden model
- No 'LLM settings override is only allowed...' error appears

**Fail:**
- Error message appears: 'LLM settings override is only allowed for published agents from agent studio'
- Response contains 400/401 error
