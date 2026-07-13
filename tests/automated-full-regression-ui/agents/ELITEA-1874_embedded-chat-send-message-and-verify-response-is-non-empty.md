---
id: ELITEA-1874
title: "Embedded chat — send message and verify response is non-empty"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
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
| 2 | Locate the embedded chat panel on the right side of the detail page | The embedded chat panel is visible |
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
