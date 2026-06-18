---
id: ELITEA-0495
title: "Verify chat messages are not duplicated when switching between conversations"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat]
requirements: []
---
# ELITEA-0495: Verify chat messages are not duplicated when switching between conversations

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** When users switch between different conversations in the chat panel, messages from the previous conversation appear duplicated in the current conversation view. This creates confusion as users see messages that don't belong to the active conversation or see their own messages repeated.

## Preconditions

User is logged into Elitea platform
At least two conversations exist with different messages in each
User has access to Chat functionality

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat page and open Conversation A. Note the exact messages and message count displayed | Conversation A loads with its specific messages visible. Message count and content are noted |
| 2 | Send a new message in Conversation A (e.g., 'Message in Conv A') and wait for AI response | Message is sent and AI responds. Updated message count is noted (e.g., N messages) |
| 3 | Click on Conversation B in the conversation list panel to switch to it | Conversation B loads showing only its own messages, with no messages from Conversation A visible |
| 4 | Verify message count in Conversation B matches its expected count (different from Conversation A) | Message count is correct for Conversation B. No duplicate or foreign messages appear |
| 5 | Switch back to Conversation A by clicking it in the conversation list | Conversation A loads with exactly the same messages as before (including the one sent in step 2), no duplicates |
| 6 | Rapidly switch between Conversation A and Conversation B 3-4 times | Each conversation consistently shows only its own messages with correct counts, no duplication occurs |
| 7 | After rapid switching, stay on Conversation B and scroll through all messages | Only Conversation B messages are shown. No messages from Conversation A have leaked into the view |
| 8 | Refresh the page and navigate back to Conversation A | Conversation A shows the correct messages with no duplicates even after page refresh |
| 9 | Open Conversation B in a new browser tab and compare message lists between both tabs | Both tabs show correct, non-duplicated messages for their respective conversations |
| 10 | In Tab 1 showing Conversation A, send a new message. Immediately switch to Tab 2 showing Conversation B and verify no cross-contamination | Tab 2 (Conversation B) shows no new messages from Conversation A. The new message only appears in Tab 1's Conversation A. No WebSocket cross-talk between conversations |
| 11 | Switch to Conversation A, send a message, and while the AI is still streaming the response, immediately switch to Conversation B | Conversation B displays correctly with no partial streaming content from Conversation A's in-progress response. Switching mid-stream does not cause duplication or content bleeding |
| 12 | Switch back to Conversation A after the mid-stream switch and verify the AI response completed correctly | Conversation A shows the complete AI response — the mid-stream switch did not truncate, duplicate, or corrupt the response. Message count is correct (N+2: original + new user msg + AI response) |
| 13 | Create a brand new Conversation C, send a message in it, then rapidly cycle through A → B → C → A and verify all three conversations maintain correct independent message states | All three conversations maintain their independent message lists with correct counts. No cross-contamination between any pair of conversations. New Conversation C shows only its own messages |

## Expected Final State

All three conversations maintain their independent message lists with correct counts. No cross-contamination between any pair of conversations. New Conversation C shows only its own messages

## Pass/Fail Criteria

PASS: Each conversation consistently displays only its own messages with correct counts through all switching scenarios including rapid switches, mid-stream switches, multi-tab, and three-conversation cycling
FAIL: Any message appears duplicated, messages from one conversation appear in another, message counts are incorrect after switching, mid-stream switching causes content bleeding, or multi-tab WebSocket cross-talk occurs
