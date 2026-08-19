---
id: ELITEA-2465
title: "Chat – Add agent with conversation starters and use a starter to send message"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_chat_agent_starters_add_remove.TestChatAddAgentWithStartersAndSendViaStarter.test_add_agent_with_starters_and_send_via_starter"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1586
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2465: Chat – Add agent with conversation starters and use a starter to send message

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Add agent with conversation starters and use a starter to send message. Success is confirmed when verify the agent's full response is received and displayed with no error.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chats section and open or create a new conversation | Target page/section loads successfully. |
| 2 | Verify the default LLM is shown in the input bar | Condition holds as described. |
| 3 | Click + and select Agents, then select an agent with conversation starters configured (e.g. "Claude B") | Control responds; expected next state is shown. |
| 4 | Verify the input bar now shows the agent name and version (e.g. "Claude B \| base") with a gear icon and X icon | Condition holds as described. |
| 5 | Verify the PARTICIPANTS panel shows the AGENTS section with the selected agent | Condition holds as described. |
| 6 | Verify conversation starter buttons are displayed above the message input field (maximum 4 starters) | Condition holds as described. |
| 7 | Hover over a starter button with truncated text and verify a tooltip shows the full text | Action completes without error and produces the expected UI state. |
| 8 | Click on a conversation starter (e.g. "here is your task: Explain Exponential Backoff") | Control responds; expected next state is shown. |
| 9 | Verify the full starter text is inserted into the message input field and is editable | Condition holds as described. |
| 10 | Click the Send button | Control responds; expected next state is shown. |
| 11 | Verify the message is sent and appears in the conversation directed "to [Agent Name]" | Condition holds as described. |
| 12 | Verify the agent begins processing with a response generation indicator | Condition holds as described. |
| 13 | Verify the LLM model label is shown on the agent's response | Condition holds as described. |
| 14 | Verify a "Thinking" section is visible and expanding during generation | Condition holds as described. |
| 15 | Verify the agent's full response is received and displayed with no error | Condition holds as described. |

---

## Expected Final State

Verify the agent's full response is received and displayed with no error.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Add agent with conversation starters and use a starter to send message.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
