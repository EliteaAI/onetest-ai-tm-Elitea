---
id: ELITEA-0450
title: "Steps Limit Persists Across Multiple Messages in the Same Conversation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3292]
---
# ELITEA-0450: Steps Limit Persists Across Multiple Messages in the Same Conversation

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that a configured Steps Limit persists across multiple sequential messages within the same conversation session and is not reset between turns.

**Coverage:**
- Steps Limit remains applied for the full conversation session
- Multiple sequential tool-using turns each respect the same limit
- Limit value shown in Model Settings is unchanged between messages

## Preconditions

- Logged in to {{base_url}}
- Private project selected
- Artifact Toolkit configured with default bucket
- Browser: Chrome (latest)

## Test Data

- Steps Limit: 4
- Prompt 1: "list files 10 times using separate tool calls"
- Prompt 2: "list files 10 times using separate tool calls"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation with Artifact Toolkit added. Open Model Settings and set STEPS LIMIT to '4'. Click Apply. | Modal closes. Steps Limit is set to 4. |
| 2 | Send Prompt 1 in the chat. | Execution stops at 4 iterations with message 'Maximum tool execution iterations (4) reached. Stopping tool execution.' |
| 3 | Send Prompt 2 in the same conversation without reopening Model Settings. | Execution again stops at 4 iterations with the same error message. |
| 4 | Open Model Settings modal again without making changes. | STEPS LIMIT field still shows '4'. |

## Expected Final State

STEPS LIMIT field still shows '4'.

## Pass/Fail Criteria

**Pass:**
- Both Prompt 1 and Prompt 2 are stopped at exactly 4 iterations
- Steps Limit modal shows 4 after both messages without any change

**Fail:**
- Second message executes more than 4 iterations (limit reset between turns)
- Modal shows a different value after messages are sent
- Any crash or unexpected behavior
