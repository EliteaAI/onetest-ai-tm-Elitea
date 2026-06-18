---
id: ELITEA-0421
title: "Chat Controls Remain Fully Functional After Cancelling Warning Modal"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:chat, ui]
requirements: [ProjectAlita/projectalita.github.io#3933]
---
# ELITEA-0421: Chat Controls Remain Fully Functional After Cancelling Warning Modal

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that after clicking Cancel on the in-progress generation warning modal, the current conversation is fully usable: generation continues and the input field, send button, and + Create button are not disabled.

**Coverage:**
- User remains on the current conversation after Cancel
- Generation is not interrupted after Cancel
- Message input field is active and accepts input
- Send button is enabled
- + Create button is enabled

## Preconditions

- Logged in to {{base_url}} with Chat access
- Existing conversation with an LLM model or agent participant
- Chrome (latest)

## Test Data

- Prompt: "Write a detailed 10-paragraph essay about climate change."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open a conversation with an LLM model or agent. | Conversation is open. |
| 2 | Send: "Write a detailed 10-paragraph essay about climate change." | Response begins streaming. |
| 3 | While streaming, click + Create in the Chat sidebar. | Warning modal appears: "Output is still generating. Switching now will stop it and you may lose progress. Switch anyway?" |
| 4 | Click Cancel. | Modal closes. User stays on the current conversation. |
| 5 | Observe the response area. | The response is still streaming or has completed normally — it was not cut off or frozen. |
| 6 | Click the message input field. | Input field accepts focus and text can be typed. |
| 7 | Inspect the Send button state. | Send button is enabled and not greyed out. |
| 8 | Inspect the + Create button in the sidebar. | + Create button is enabled and responds to click. |

## Expected Final State

+ Create button is enabled and responds to click.

## Pass/Fail Criteria

**Pass:**
- User remains on the current conversation after Cancel
- Generation continues normally without interruption
- Message input field is active and accepts text
- Send button is enabled
- + Create button is enabled and clickable

**Fail:**
- User is redirected despite clicking Cancel
- Generation stops, freezes, or produces an error after Cancel
- Message input field is disabled or does not accept text
- Send button is greyed out or unresponsive
- + Create button is disabled or unresponsive after Cancel
