---
id: ELITEA-2677
title: "Stop button does not corrupt or delete existing chat history"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.6, issue:5000]
requirements: [EliteaAI/elitea_issues#5000]
---
# ELITEA-2677: Stop button does not corrupt or delete existing chat history

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that using Stop button does not corrupt existing chat history or cause data loss in the chat thread — only the last user message sent before clicking Stop should be removed.

## Preconditions

- User is logged in to `{{base_url}}`
- Chat thread with at least 5 previous messages and responses exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test Message | "Test message for stop" |
| Minimum Previous Messages | 5 message pairs (user + AI/agent response) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open chat interface with existing conversation history | Chat interface loads with existing messages visible |
| 2 | Count and note the total number of messages in the thread | Message count is recorded (e.g., 10 messages: 5 user + 5 responses) |
| 3 | Type "Test message for stop" in the input field | Text appears in the input field |
| 4 | Click Send button | Message appears in the chat thread; response processing starts |
| 5 | Click Stop button during processing | Stop button is clicked successfully |
| 6 | Verify only the last user message ("Test message for stop") is removed | Only the last message is removed; all previous messages remain intact |
| 7 | Count the messages in the thread | Message count matches the original count (before sending the stopped message) |
| 8 | Scroll through the entire chat history | All previous messages (before the stopped message) are displayed correctly with no duplicates or missing messages |
| 9 | Refresh the page (F5 or Ctrl+R) | Page reloads successfully |
| 10 | Verify chat history after refresh | Chat history persists correctly with all original messages intact |
| 11 | Verify no duplicate or missing messages appear | Chat thread is consistent and accurate |

## Expected Final State

Chat thread contains all original messages before the stopped message. No data loss, corruption, or duplicate messages. Message count matches the state before sending the stopped message.

## Pass/Fail Criteria

**Pass:**
- Only the last sent message is removed from the thread
- All previous messages remain intact and visible
- Message count is correct
- Chat history persists after page refresh
- No duplicate or missing messages

**Fail:**
- Previous messages are deleted or corrupted
- Message count is incorrect
- Chat history is lost after refresh
- Duplicate messages appear
- Messages are out of order
