---
id: ELITEA-0503
title: "Chat Message Input Methods"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_chat_interface.TestSendingMessages.test_send_text_message
  - tests.ui.chat.test_chat_interface.TestSendingMessages.test_send_message_with_enter_key
  - tests.ui.chat.test_chat_interface.TestSendingMessages.test_cannot_send_empty_message
tags: []
requirements: []
---
# ELITEA-0503: Chat Message Input Methods

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can send text messages via Send button and Enter key, Shift+Enter adds new lines, and empty messages are blocked.

## Preconditions

- User logged into Elitea
- Chat conversation open

## Test Data

- URL: {{base_url}}
- Test message: Hello, testing message input

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Type text message, click Send | Message sent, appears in history |
| ? | Type message, press Enter | Message sent |
| ? | Type message, press Shift+Enter | New line added, message not sent |
| ? | Try to send empty message | Send button disabled or no action |

## Expected Final State

Send button disabled or no action

## Pass/Fail Criteria

**Pass:**
- Send button sends message
- Enter key sends message
- Shift+Enter adds newline without sending
- Empty message prevented

**Fail:**
- Send doesn't work
- Enter doesn't send
- Shift+Enter sends instead of newline
- Empty message sent
