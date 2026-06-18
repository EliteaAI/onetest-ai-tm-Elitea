---
id: ELITEA-0548
title: "Edit icon visible only on last user message in multi-message conversation"
priority: critical
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0548: Edit icon visible only on last user message in multi-message conversation

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Edit (pencil) icon appears exclusively on the most recent user message and relocates correctly when a new message is sent.

**Coverage:**
- Icon present on last user message
- Icon absent on older user messages
- Icon absent on assistant/system/tool messages
- Icon moves to new last message after sending another message

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- An existing Chat Conversation with at least 3 user-assistant message exchanges

## Test Data

- Chat Conversation with 3+ user messages and corresponding LLM responses
- New message to send: "What is the capital of France?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat → Conversations. Open a conversation with 3+ user messages. | Conversation loads with full message history visible. |
| 2 | Inspect all user messages in the conversation for the presence of a Pencil/Edit icon. | Only the last (most recent) user message displays the Edit icon. Older user messages do not have it. |
| 3 | Inspect all assistant/LLM response messages for the Edit icon. | No assistant message has an Edit icon. |
| 4 | Inspect any system or tool messages (if present) for the Edit icon. | No system/tool message has an Edit icon. |
| 5 | Send a new message: "What is the capital of France?" and wait for the LLM response. | New message appears as the last user message. |
| 6 | Verify which message now displays the Edit icon. | The Edit icon has moved to the newly sent message. The previously-last message no longer has the icon. |

## Expected Final State

The Edit icon has moved to the newly sent message. The previously-last message no longer has the icon.

## Pass/Fail Criteria

**Pass:**
- Edit icon is visible only on the last user message at all times
- Icon moves correctly when a new message is sent
- No other message type shows the Edit icon

**Fail:**
- Edit icon appears on older user messages
- Edit icon appears on assistant/system/tool messages
- Edit icon does not relocate after sending a new message
