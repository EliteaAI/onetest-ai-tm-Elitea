---
id: ELITEA-0647
title: "User sends a message via the Send button and receives a complete assistant response"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [critical-path, send-receive, regression, R-2.0.3, smoke]
requirements: [EliteaAI/elitea_issues#4775, EliteaAI/elitea_issues#4773]
---
# ELITEA-0647: User sends a message via the Send button and receives a complete assistant response

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** The complete end-to-end send and receive cycle: type a message, click Send, the message appears in the conversation, a loading indicator shows while the assistant is thinking, and the full assistant response replaces the indicator. This is the most fundamental flow — if this breaks, the feature is unusable.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant is enabled and an active agent is configured in the Support Assistant project
- Support Assistant panel is open

## Test Data

- Message to send: "What is ELITEA?"
- Expected: any valid response from the configured agent about the ELITEA platform

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click inside the message input field and type "What is ELITEA?". | The text "What is ELITEA?" appears in the input field. The Send button becomes active. |
| 2 | Click the Send button. | The message is submitted. The input field clears. |
| 3 | Observe the message list immediately after clicking Send. | The user message "What is ELITEA?" appears in the conversation on the right side (or visually distinct as a user bubble) with a timestamp. |
| 4 | Observe the assistant area while the response is being generated. | A loading indicator (animated "..." or spinner) appears on the assistant side. The message input field is not editable. The Send button is inactive. |
| 5 | Wait for the assistant to finish generating. | The loading indicator disappears and the full response text appears in the conversation below the user message. |
| 6 | Observe the state of the message input field after the response is shown. | The input field is editable again. The Send button is inactive (input is empty, ready for the next message). |

## Expected Final State

The input field is editable again. The Send button is inactive (input is empty, ready for the next message).

## Pass/Fail Criteria

Pass:
- User message appears in the conversation immediately after sending
- Loading indicator is shown while the assistant is generating
- Input field and Send button are locked during generation
- Full response text appears after generation completes
- Input field re-enables after the response is complete

Fail:
- Message is not sent or does not appear in the conversation
- No loading indicator is shown
- Input remains editable during generation (double-send risk)
- No response ever appears (generation hangs or fails silently)
- Input stays locked after the response has completed
