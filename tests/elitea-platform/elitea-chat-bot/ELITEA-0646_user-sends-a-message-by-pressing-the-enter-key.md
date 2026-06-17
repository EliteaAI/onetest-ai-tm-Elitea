---
id: ELITEA-0646
title: "User sends a message by pressing the Enter key"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [keyboard-shortcut, send-receive, R-2.0.3, smoke]
requirements: [#4775]
---
# ELITEA-0646: User sends a message by pressing the Enter key

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Pressing Enter in the message input field must send the message — this is the standard interaction model for any chat interface. If Enter does not work, keyboard-first users cannot send messages at all without using the mouse.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open

## Test Data

- Message to send: "How do I create an agent in ELITEA?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click inside the message input field and type "How do I create an agent in ELITEA?". | Text appears in the input. Send button becomes active. |
| 2 | Press the Enter key (not Shift+Enter). | The message is submitted. The outcome is identical to clicking the Send button. |
| 3 | Observe the conversation after pressing Enter. | "How do I create an agent in ELITEA?" appears as a user message. The input field clears. The loading indicator appears on the assistant side. |
| 4 | Wait for the assistant response to appear. | Full response text renders in the conversation. Input field re-enables. |

## Expected Final State

Full response text renders in the conversation. Input field re-enables.

## Pass/Fail Criteria

Pass:
- Enter key submits the message
- The full send/receive cycle completes identically to using the Send button

Fail:
- Enter key inserts a new line instead of sending
- Nothing happens when Enter is pressed
- Message appears duplicated or an error is shown
