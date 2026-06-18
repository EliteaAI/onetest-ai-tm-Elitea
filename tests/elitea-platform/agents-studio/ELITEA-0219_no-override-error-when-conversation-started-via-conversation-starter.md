---
id: ELITEA-0219
title: "No Override Error When Conversation Started via Conversation Starter"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0219: No Override Error When Conversation Started via Conversation Starter

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that no "LLM settings override is only allowed for published agents from agent studio" error appears when a conversation is started via a Conversation Starter button with a model override active.

**Coverage:**
- Override-restriction error does not fire for conversations started via Conversation Starter buttons

## Preconditions

- Published agent with Conversation Starters configured is open in chat (agentId=16)

## Test Data

Override model: Anthropic Claude Sonnet 4.5
Conversation Starter: "Tell me about Elitea" (or any available starter)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open published agent in chat. | Conversation Starter buttons are visible. |
| 2 | Switch model to Anthropic Claude Sonnet 4.5. | Toolbar shows updated model. |
| 3 | Click a Conversation Starter button. | Message is sent to the agent. |
| 4 | Read the full response. | Response is a valid answer, not an error. |
| 5 | Confirm no 'LLM settings override is only allowed...' text appears in the response. | No such text. |

## Expected Final State

No such text.

## Pass/Fail Criteria

**Pass:**
- Agent returns a normal response to the Conversation Starter message
- No override-restriction error message in the response

**Fail:**
- Response contains: 'LLM settings override is only allowed for published agents from agent studio'
