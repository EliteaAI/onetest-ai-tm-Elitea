---
id: ELITEA-0151
title: "Chat — Conversation history intact after agent version unpublished"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agent-publishing, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4701]
---
# ELITEA-0151: Chat — Conversation history intact after agent version unpublished

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that prior conversation messages remain fully visible and intact when a conversation is reopened after its agent has been unpublished.

**Coverage:**
- All prior messages visible and in correct order after unpublish
- Agent reference preserved in the conversation (not shown as broken or unknown)

## Preconditions

- Logged in to {{base_url}}
- Agent "Test Publishing" has been unpublished (any scenario — all versions or partial)
- Existing conversation has at least 3 user messages and 3 agent responses
- Content of those messages noted down before unpublishing for comparison

## Test Data

- Agent name: "Test Publishing"
- Note at least 3 user messages and 3 agent responses before the agent is unpublished

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Before unpublishing: note the content of the last 3 user messages and 3 agent responses in the conversation. | Messages recorded for later comparison. |
| 2 | Unpublish the agent. Then open the existing conversation. | Conversation view loads. |
| 3 | Scroll through the full message history. | All previously noted user and agent messages are present, in correct order, with correct content. |
| 4 | Check the agent name/reference in the conversation header or participant area. | Agent name is still displayed — not shown as broken, missing, or 'unknown'. |

## Expected Final State

Agent name is still displayed — not shown as broken, missing, or 'unknown'.

## Pass/Fail Criteria

**Pass:**
- All prior messages present, in order, with correct content
- Agent reference visible and not broken

**Fail:**
- Any prior message is missing, corrupted, or out of order
- Agent reference shown as broken or 'unknown'
