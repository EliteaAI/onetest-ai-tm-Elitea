---
id: ELITEA-0215
title: "Model Settings Override Is Per-Session Only — Resets on New Conversation"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0215: Model Settings Override Is Per-Session Only — Resets on New Conversation

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that LLM model and settings overrides are scoped to the current session only — starting a new conversation with the same agent reverts to the agent's default model and settings.

**Coverage:**
- New conversation resets model to agent default
- Session override does not persist across new conversations

## Preconditions

- Published agent default model: Anthropic Claude 4.5 Sonnet
- User has overridden model to GPT-5.2 in a current session

## Test Data

Override model: GPT-5.2
Agent default: Anthropic Claude 4.5 Sonnet

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open published agent, switch model to GPT-5.2, send a message. | Response received with GPT-5.2. |
| 2 | Close the current conversation or start a new conversation with the same published agent. | New conversation initializes. |
| 3 | Observe the model selector in the new conversation's chat toolbar. | Model shows Anthropic Claude 4.5 Sonnet (agent default), not GPT-5.2. |

## Expected Final State

Model shows Anthropic Claude 4.5 Sonnet (agent default), not GPT-5.2.

## Pass/Fail Criteria

**Pass:**
- New conversation shows the agent's default model
- Override from previous session is not carried over

**Fail:**
- New conversation inherits the GPT-5.2 override from the previous session
- Override is persisted across conversations
