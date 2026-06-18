---
id: ELITEA-0229
title: "LLM Model Override Works When Conversation Started via Conversation Starter"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0229: LLM Model Override Works When Conversation Started via Conversation Starter

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the LLM model override is fully functional when the conversation is initiated by clicking a Conversation Starter button.

**Coverage:**
- Model override applied to sessions started via Conversation Starter
- No errors when sending messages in such sessions with overridden model

## Preconditions

- Published agent has at least one Conversation Starter configured (e.g. "Help me configure Jira toolkit?")
- Agent: Assistant for ELITEA Documentation (agentId=16)

## Test Data

Conversation Starter: "Help me configure Jira toolkit?"
Override model: Anthropic Claude 4.6 Sonnet

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open published agent in chat. | Conversation Starter buttons are visible. |
| 2 | Before clicking a starter, switch the model to Anthropic Claude 4.6 Sonnet via the model selector. | Toolbar shows new model. |
| 3 | Click the 'Help me configure Jira toolkit?' Conversation Starter button. | Message is sent to the agent. |
| 4 | Observe the response — check for errors or success. | A valid response is returned, no access errors. |

## Expected Final State

A valid response is returned, no access errors.

## Pass/Fail Criteria

**Pass:**
- Model override is applied when session starts from a Conversation Starter
- Agent returns a valid response without any model-access or override-restriction errors

**Fail:**
- Error 'LLM settings override is only allowed for published agents from agent studio' appears
- Response fails with 400/401 error
