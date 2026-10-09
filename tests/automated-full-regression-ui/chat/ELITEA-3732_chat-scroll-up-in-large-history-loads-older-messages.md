---
id: ELITEA-3732
title: "Chat – Scroll Up in Conversation with Large History Loads Older Messages"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [manual:UI:regression, feat:chat]
requirements: []
---

# ELITEA-3732: Chat – Scroll Up in Conversation with Large History Loads Older Messages

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that when opening a conversation with a large message history (50+ messages), scrolling up dynamically loads older messages and allows the user to reach the very first message in the conversation.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least 50 messages exists (can be created during test setup).
- The conversation contains identifiable first and last messages (e.g., "Message 1" and "Message 50").

---

## Test Data

| Field | Value |
|-------|-------|
| Conversation name | Large History Test |
| Number of messages | 50+ |
| First message content | "This is message number 1" |
| Last message content | "This is message number 50" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Private or Team project and go to Chats | Chats page is displayed |
| 2 | Locate the conversation with 50+ messages in the conversation list | Conversation is visible in the list |
| 3 | Click on the conversation to open it | Conversation opens; most recent messages are displayed at the bottom |
| 4 | Verify the most recent message (e.g., "Message 50") is visible | Last message is displayed |
| 5 | Scroll up slowly in the message area | Older messages begin to load and appear above the currently visible messages |
| 6 | Continue scrolling up | More older messages load dynamically as the user scrolls |
| 7 | Keep scrolling until reaching the top of the conversation | The very first message (e.g., "This is message number 1") is visible |
| 8 | Verify no loading spinner is stuck or infinite loading occurs | Loading completes; all messages are accessible |
| 9 | Scroll back down to the bottom | Recent messages are still visible and accessible |
| 10 | Verify message order is preserved (oldest at top, newest at bottom) | Messages appear in chronological order |

---

## Expected Final State

The conversation with large history loads all messages when scrolling up. The user can reach the very first message in the conversation without the history being truncated or cut off.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Older messages load dynamically when scrolling up.
- The first message in the conversation is reachable.
- No messages are missing or truncated from the history.
- No infinite loading or stuck spinners occur.

**Fail:**
- Scrolling up does not load older messages.
- The conversation history is truncated and the first message cannot be reached.
- Loading spinner gets stuck or infinite loading occurs.
- Messages are missing from the history.
- Application crashes or freezes when scrolling through large history.

---

## Notes

- This test addresses a reported bug where conversations with large message history could not be scrolled to view older messages.
- The lazy loading / pagination mechanism for chat messages should ensure all historical messages are accessible.
- Consider testing with conversations of varying sizes (50, 100, 200+ messages) to verify scalability.
