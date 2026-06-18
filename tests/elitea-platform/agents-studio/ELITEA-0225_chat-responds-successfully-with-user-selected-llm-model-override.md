---
id: ELITEA-0225
title: "Chat Responds Successfully with User-Selected LLM Model Override"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0225: Chat Responds Successfully with User-Selected LLM Model Override

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that after switching the LLM model in a published agent session, sending a message returns a successful response using the overridden model without errors.

**Coverage:**
- No 401/400/model-access-denied errors after model switch
- Response is generated using the selected model

## Preconditions

- Published agent is open in chat
- User has switched model from default to a different one

## Test Data

Switch model to: GPT-5.2
Test message: "Hello, what can you help me with?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open published agent in chat and switch model to GPT-5.2. | Toolbar shows GPT-5.2. |
| 2 | Type 'Hello, what can you help me with?' in the chat input and send. | Message is sent. |
| 3 | Observe the response. | A valid, non-error response is returned from the agent. |
| 4 | Check that no error message appears (e.g. no 401, 400, 'team not allowed to access model', or 'LLM settings override' errors). | No error messages in the chat. |

## Expected Final State

No error messages in the chat.

## Pass/Fail Criteria

**Pass:**
- Agent responds normally to the message
- No error codes or access-denied messages in the response

**Fail:**
- Response contains error: 401, 400, 'team not allowed to access model', 'invalid model name', or any access restriction message
