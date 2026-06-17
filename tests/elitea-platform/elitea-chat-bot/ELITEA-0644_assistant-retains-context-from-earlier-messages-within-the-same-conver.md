---
id: ELITEA-0644
title: "Assistant retains context from earlier messages within the same conversation"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [conversation-memory, context-retention, multi-turn, R-2.0.3]
requirements: [EliteaAI/elitea_issues#4775, EliteaAI/elitea_issues#4776]
---
# ELITEA-0644: Assistant retains context from earlier messages within the same conversation

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** The assistant must remember what was said earlier in the same session so that the user can ask follow-up questions naturally. Without this, every message is treated as a fresh, isolated request — which makes the feature unusable for any real support scenario.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open in a fresh or new session
- The configured agent supports multi-turn conversation (has memory of the current session)

## Test Data

- First message: "My name is TestUser123"
- Second message: "What is my name?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click New Chat to start a clean session (if prior messages exist). Verify only the welcome message is shown. | New empty session with welcome message. |
| 2 | Type "My name is TestUser123" and send it. | Message appears in the conversation as a user message. Loading indicator shows. |
| 3 | Wait for the assistant to respond. | The assistant's response acknowledges or confirms the name "TestUser123". |
| 4 | Type "What is my name?" as a follow-up and send it. | Message appears below the first exchange. Loading indicator shows. |
| 5 | Wait for the assistant's second response. | The assistant's response includes "TestUser123", demonstrating it has retained context from the first message. |
| 6 | Observe the conversation from top to bottom. | All four entries are visible in the correct order: first user message → first response → second user message → second response. |

## Expected Final State

All four entries are visible in the correct order: first user message → first response → second user message → second response.

## Pass/Fail Criteria

Pass:
- The assistant's response to "What is my name?" references "TestUser123"
- All four messages visible in chronological order

Fail:
- The assistant says it does not know the name or responds as if the conversation just started
- Messages appear out of order or earlier messages disappear from the list
