---
id: ELITEA-0230
title: "Model Override Does Not Modify Published Agent's Underlying Configuration"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0230: Model Override Does Not Modify Published Agent's Underlying Configuration

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that changing the LLM model in a chat session does not alter the published agent's saved author configuration.

**Coverage:**
- Agent configuration remains unchanged after session model override
- Override is session-scoped only

## Preconditions

- User has access to the agent's edit/configuration page
- Agent default model is known (e.g. Anthropic Claude 4.5 Sonnet)

## Test Data

Agent: Assistant for ELITEA Documentation (agentId=16)
Author-configured model: Anthropic Claude 4.5 Sonnet
Override model: GPT-5.4

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note the agent's current LLM model in its configuration page: Anthropic Claude 4.5 Sonnet. | Configuration is recorded. |
| 2 | Open the agent in chat, switch model to GPT-5.4, and send a message. | Response received with GPT-5.4. |
| 3 | Return to the agent's configuration/edit page and check the LLM model field. | Model still shows Anthropic Claude 4.5 Sonnet. |

## Expected Final State

Model still shows Anthropic Claude 4.5 Sonnet.

## Pass/Fail Criteria

**Pass:**
- Agent configuration page still shows the author's original model after chat session override
- No changes persisted to the agent's saved settings

**Fail:**
- Agent configuration page shows GPT-5.4 instead of Anthropic Claude 4.5 Sonnet
