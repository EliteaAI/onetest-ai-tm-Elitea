---
id: ELITEA-0485
title: "Validate Code File Attachment Persists in Conversation History"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [programming-files, feat:attachments, data-persistence, story:3671, r-2.0.1, history]
requirements: [ProjectAlita/projectalita.github.io#3671]
---
# ELITEA-0485: Validate Code File Attachment Persists in Conversation History

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after sending a message with a code file attachment, the attachment is correctly preserved in the conversation history. When the user scrolls back through past messages, the code file attachment should be visible in the user's message.

## Preconditions

1. User is logged into Elitea platform
2. A Chat conversation exists with previous messages
3. Backend returns `.js` in `code_types` for the project
4. A JavaScript file `script.js` (~500 bytes) is available

## Test Data

- `script.js`: A JavaScript file with a simple function

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing Chat conversation that already has previous messages | Conversation history is visible |
| 2 | Click attachment button and select `script.js` | File attaches. Count: 1. |
| 3 | Type: "Can you explain what this JavaScript function does?" | Text appears in input |
| 4 | Send the message | Message and attachment are sent; AI responds |
| 5 | After the AI responds, scroll up in the conversation to find the user's sent message | The user's sent message is visible |
| 6 | Verify that the `script.js` attachment is shown within the user's sent message in history | The `script.js` attachment chip/label is visible in the user's message bubble in the conversation history |
| 7 | Navigate away from the conversation and return to it | The conversation reloads |
| 8 | Verify the `script.js` attachment is still visible in the message history after reload | The attachment persists after navigation and reload |

## Expected Final State

The attachment persists after navigation and reload

## Pass/Fail Criteria

- PASS: Attachment is visible in message history immediately after sending; attachment persists after navigation and reload; attachment label shows the correct filename
- FAIL: Attachment disappears from message history after the AI responds; attachment is not visible after page reload; attachment shows incorrect filename or missing entirely
