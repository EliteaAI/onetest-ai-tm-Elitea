---
id: ELITEA-0493
title: "Verify chat input field retains focus after sending a message"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat]
requirements: []
---
# ELITEA-0493: Verify chat input field retains focus after sending a message

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** After sending a message in chat, the text input field loses focus. Users must manually click back into the input area before they can type their next message, disrupting the conversational flow and reducing productivity.

## Preconditions

User is logged into Elitea platform
A conversation exists or can be created
User has access to Chat functionality

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat page and open an existing conversation or create a new one | Chat page loads with the message input textarea visible and focused (cursor blinking in input) |
| 2 | Type a message in the input field and press Enter to send it | Message is sent successfully and appears in the message list |
| 3 | Without clicking anywhere, immediately check if the cursor is still in the input field (look for blinking cursor indicator) | Input field retains focus with cursor blinking, ready for the next message |
| 4 | Without clicking the input field, start typing a second message immediately | Characters appear in the input field without needing to click it first — focus was retained |
| 5 | Send the second message using the Send button (click) instead of Enter | Message is sent and input field retains focus afterward |
| 6 | Wait for the AI response to complete, then check if input field still has focus | After AI response finishes streaming, input field still has focus and is ready for typing |
| 7 | Send a third message and while the AI is still responding (streaming), check input field focus | Input field remains focused even during AI response streaming — user can type next message while AI responds |
| 8 | Switch to a different conversation and immediately try typing without clicking the input field | After switching conversations, input field is auto-focused and ready for typing |

## Expected Final State

After switching conversations, input field is auto-focused and ready for typing

## Pass/Fail Criteria

PASS: Input field retains focus in all scenarios (Enter send, button send, after AI response, after conversation switch) and user can type immediately
FAIL: Input field loses focus after any send action requiring user to click the input area before typing next message
