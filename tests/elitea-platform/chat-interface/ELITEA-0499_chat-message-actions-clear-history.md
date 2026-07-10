---
id: ELITEA-0499
title: "Chat Message Actions - Clear History"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_chat_interface.TestConversationUIElements.test_clear_chat_history
tags: []
requirements: []
---
# ELITEA-0499: Chat Message Actions - Clear History

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify chat message clear history functionality.

**Coverage:**
- Clear chat history button works
- All messages removed after clearing

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one conversation exists (create one manually if needed)
- AI model is available for generating responses
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Test message: Test message before clear

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open an existing conversation. Send a message (e.g., 'Test message before clear') and wait for the AI response. | Both the user message and AI response appear in the chat. The message count is greater than 0. |
| 2 | Look for the 'Clear chat history' button (eraser/trash icon) in the chat header toolbar area. Verify it is enabled. | The Clear chat history button is visible and enabled. |
| 3 | Click the Clear chat history button. | A confirmation dialog appears with 'Cancel' and 'Confirm' options. |
| 4 | Click 'Confirm' in the dialog. | The dialog closes. The clear operation is initiated. |
| 5 | Reload the page. Count the messages in the chat. | The message count is 0. All previous messages have been removed. |

## Expected Final State

The message count is 0. All previous messages have been removed.

## Pass/Fail Criteria

**Pass:**
- Message sent and AI response received before clearing
- Clear button enabled when messages exist
- Confirmation dialog appears on click
- All messages removed after confirm + reload
- Message count returns to 0

**Fail:**
- Clear button disabled even with messages
- Confirmation dialog doesn't appear
- Messages persist after clearing + reload
- Clear operation causes error or crash
