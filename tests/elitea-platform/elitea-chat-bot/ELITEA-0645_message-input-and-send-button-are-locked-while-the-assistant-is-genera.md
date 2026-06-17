---
id: ELITEA-0645
title: "Message input and Send button are locked while the assistant is generating a response"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [double-send-prevention, loading-state, input-state, R-2.0.3]
requirements: [#4775]
---
# ELITEA-0645: Message input and Send button are locked while the assistant is generating a response

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Once a message is sent and the assistant is generating a response, the user must not be able to send another message. This prevents duplicate API calls, out-of-order responses, and conversation corruption.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open
- The configured agent takes at least 2–3 seconds to respond, providing an observable window during generation

## Test Data

- Message to send: "List all the main features of ELITEA in detail" (worded to produce a longer response time)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type "List all the main features of ELITEA in detail" in the input field and send it by clicking Send or pressing Enter. | Message is submitted. Loading indicator appears on the assistant side. |
| 2 | While the loading indicator is still visible, click inside the message input field and try to type any text. | No text can be entered. The input field is not interactive. |
| 3 | While the loading indicator is still visible, click the Send button. | The Send button does not respond. No duplicate message is sent. No second loading indicator appears. |
| 4 | While the loading indicator is still visible, press the Enter key. | Nothing happens. |
| 5 | Wait for the assistant to finish generating and the full response to appear. | Loading indicator disappears. Full response is shown in the conversation. |
| 6 | Now click the input field and try to type a new message. | The input field accepts text normally. The composer is fully restored to an interactive state. |

## Expected Final State

The input field accepts text normally. The composer is fully restored to an interactive state.

## Pass/Fail Criteria

Pass:
- Input field is not editable during response generation
- Send button does not respond to clicks during generation
- No duplicate messages appear in the conversation
- Input and Send button are both fully functional again after generation completes

Fail:
- User can type in the input field while the assistant is generating
- Clicking Send during generation submits a second message (double-send)
- Input field remains locked after the response has completed
