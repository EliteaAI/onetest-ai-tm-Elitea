---
id: ELITEA-1874
title: "Embedded chat — send message and verify response is non-empty"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_embedded_chat_send_message.TestAgentEmbeddedChatSendMessage.test_send_message_via_enter_and_verify_non_empty_response
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1292
---

# ELITEA-1874: Embedded chat — send message and verify response is non-empty

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that the embedded chat panel on the agent detail page accepts user messages and returns a non-empty, expected response from the agent.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent exists with instructions: "You are a helpful assistant. Reply only with: PONG"

---

## Test Data

| Field | Value |
|-------|-------|
| Agent instructions | You are a helpful assistant. Reply only with: PONG |
| User message | PING |
| Expected response content | PONG |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an existing agent's detail page with instructions "You are a helpful assistant. Reply only with: PONG" | The agent detail page loads |
| 2 | Click the "Test Agent" toolbar button to open the embedded chat panel | The embedded chat panel opens next to the configuration and is visible |
| 3 | Type "PING" in the chat input | The input field displays "PING" |
| 4 | Press Enter (without Shift) | The message is submitted |
| 5 | Wait for the assistant response to appear and stabilise | The assistant response is fully rendered |
| 6 | Verify the response is non-empty and contains "PONG" | The response text is non-empty and contains "PONG" |
| 7 | Verify the input field is cleared after sending | The chat input field is empty |

---

## Expected Final State

The chat panel shows the sent message "PING" and a response containing "PONG". The input field is cleared and ready for the next message.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The agent response is non-empty and contains "PONG"; the input field is cleared.

**Fail:**
- Any step produces an error or unexpected result.
- The response is empty, missing "PONG", or the input field is not cleared after sending.
