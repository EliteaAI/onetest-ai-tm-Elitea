---
id: ELITEA-0413
title: "User Can Successfully Send New Messages After Send Button Restoration Post-Summarization"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:context-management, feat:chat, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3984]
---
# ELITEA-0413: User Can Successfully Send New Messages After Send Button Restoration Post-Summarization

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that once the Send button is restored following summarization, the user can successfully send additional messages and receive responses — confirming the chat is fully functional and not just visually corrected.

**Coverage:**
- Post-summarization Send button is functionally active (not merely cosmetic)
- New messages are accepted and processed after button restoration
- Button cycles correctly on subsequent turns: Send → Terminate → Send
- Context Budget widget accurately reflects updated state after new messages

## Preconditions

- Logged in to {{base_url}} with Editor/Admin role
- `context_manager` secret = `true`; Summarization toggle = ON
- A Chat conversation is active and at least one summarization event has already occurred (Send button has reverted)
- Browser: Chrome (latest)

## Test Data

- Post-restoration message 1: "What was the main topic we discussed?"
- Post-restoration message 2: "Can you provide a brief summary of our conversation?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | After a summarization event has completed and the Send button is restored, type 'What was the main topic we discussed?' in the chat input field. | Text is entered in the input field. |
| 2 | Click the Send button (or press Enter). | The message is submitted; input field clears. |
| 3 | Confirm the button transitions to Terminate during the new LLM generation. | Terminate button is shown while LLM is generating. |
| 4 | Wait for the LLM to complete the response. | A meaningful response referencing prior conversation context is returned. |
| 5 | Confirm the button reverts to Send after the response completes. | Send button is shown. |
| 6 | Type 'Can you provide a brief summary of our conversation?' and click Send. Confirm another normal Send → Terminate → Send cycle. | Second follow-up is processed without issues. |
| 7 | Verify the Context Budget widget shows updated token count and message count reflecting the two new messages. | Widget totals are incremented. |

## Expected Final State

Widget totals are incremented.

## Pass/Fail Criteria

**Pass:**
- New messages submitted successfully via the restored Send button
- LLM generates meaningful responses for each new message
- Button cycles correctly (Send → Terminate → Send) on each turn
- Context Budget widget updates to reflect new messages

**Fail:**
- Clicking the restored Send button does not submit the message
- Button appears as Send visually but functions as no-op (no request sent)
- LLM does not respond after restoration
- Context Budget widget shows stale data
