---
id: ELITEA-2177
title: "Chat – Add Agent with Conversation Starters to Conversation"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_chat_agent_starters_add_remove.TestChatAddAgentWithStartersToConversation.test_add_agent_with_starters_to_conversation"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1586
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2177: Chat – Add Agent with Conversation Starters to Conversation

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that adding an agent with conversation starters shows the starters in the conversation, allows clicking them to populate the message field, and the agent responds correctly.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent with configured conversation starters exists (e.g. 'Claude B').

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | Claude B | Conversation starter | here is your task: Explain Exponential Backoff |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, open a conversation, click + icon, select Agents, select 'Claude B' | Agent chip shown; conversation starters visible above input field (max 4) |
| 2 | Verify starters are displayed as clickable pills; hover over truncated starter to see tooltip | Full text shown in tooltip |
| 3 | Click a conversation starter (e.g. 'here is your task: Explain Exponential Backoff') | Full text inserted in message field |
| 4 | Verify text is editable and agent name/version still shown in input bar | Text editable; agent chip visible |
| 5 | Click Send | Message sent; agent processes; response shown with agent icon and LLM model label |
| 6 | Verify agent responds with reasoning/Thinking section visible | Agent response with Thinking section |

---

## Expected Final State

Conversation starters work correctly; agent responds via starter.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Starters visible; clicking populates field; agent responds.

**Fail:**
- Any step produces an error or unexpected result.
- Starters not shown or agent fails.
