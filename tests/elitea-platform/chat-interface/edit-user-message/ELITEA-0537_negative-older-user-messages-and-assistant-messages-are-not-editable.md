---
id: ELITEA-0537
title: "Negative — older user messages and assistant messages are not editable"
priority: critical
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0537: Negative — older user messages and assistant messages are not editable

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that only the last user message is editable; older messages and all assistant messages have no Edit action.

**Coverage:**
- No Edit icon on older user messages
- No Edit icon on assistant messages
- No other means to enter edit mode on non-last messages

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A conversation with 3+ user-assistant exchanges

## Test Data

- Conversation with multiple exchanges

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a conversation with 3+ exchanges. Hover over an older user message (not the last one). | No Edit icon appears. No pencil icon in the action area. |
| 2 | Hover over any assistant/LLM response message. | No Edit icon appears on any assistant message. |
| 3 | Attempt to right-click or otherwise interact with an older user message to find an edit option. | No edit functionality is accessible for non-last user messages. |

## Expected Final State

No edit functionality is accessible for non-last user messages.

## Pass/Fail Criteria

**Pass:**
- Only the last user message has the Edit icon
- No other message type or older message is editable

**Fail:**
- Edit icon appears on older user messages
- Edit icon appears on assistant messages
- An alternate path allows editing non-last messages
