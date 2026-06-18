---
id: ELITEA-0228
title: "No Override Error When Conversation Started via User's Typed Input"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0228: No Override Error When Conversation Started via User's Typed Input

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that no "LLM settings override is only allowed for published agents from agent studio" error appears when a user initiates a conversation with their own typed message and uses a model override.

**Coverage:**
- Override-restriction error does not fire for user-initiated conversations
- Backend gate correctly identifies Agent Studio published agents

## Preconditions

- Published agent is open in chat (agentId=16, sourced from Agent Studio)
- User switches model before or after typing the first message

## Test Data

Override model: Anthropic Claude Sonnet 4.5
User message: "hi"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open published agent in chat. | Chat input is available. |
| 2 | Switch model to Anthropic Claude Sonnet 4.5 via the model selector. | Toolbar updated. |
| 3 | Type 'hi' in the input field and press Send. | Message sent. |
| 4 | Read the full response from the agent. | Response is a valid reply, NOT an error message. |
| 5 | Confirm the response does NOT contain: 'LLM settings override is only allowed for published agents from agent studio'. | No such text in response. |

## Expected Final State

No such text in response.

## Pass/Fail Criteria

**Pass:**
- Agent returns a normal response
- No override-restriction error in the response

**Fail:**
- Response contains: 'LLM settings override is only allowed for published agents from agent studio'
