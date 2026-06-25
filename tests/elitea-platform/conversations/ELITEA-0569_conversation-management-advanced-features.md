---
id: ELITEA-0569
title: "Conversation Management - Advanced Features"
priority: high
type: functional
module: conversations
status: ready
execution_type: automated
automation_test_id:
  - test_conversation_management.py:TestCreateConversation.test_new_conversation_default_settings
  - test_conversation_management.py:TestConversationList.test_click_conversation_to_open
  - test_conversation_management.py:TestConversationList.test_conversation_appears_in_list
  - test_conversation_management.py:TestConversationList.test_search_conversations_button
  - test_conversation_management.py:TestConversationNavigation.test_send_message_persists_conversation
  - test_conversation_management.py:TestConversationParticipants.test_add_teammate_to_conversation
  - test_conversation_management.py:test_multiple_conversations_listed
  - test_conversation_management.py:test_navigate_between_conversations
tags: []
requirements: []
---
# ELITEA-0569: Conversation Management - Advanced Features

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify advanced conversation management features: default settings, navigation, search, multiple conversations, adding teammates.

**Coverage:**
- New conversation has default settings (model, temperature, etc.)
- Conversation appears in list after creation
- Click conversation to open chat
- Search conversations button functional
- Navigate between multiple conversations
- Send message persists in conversation history
- Multiple conversations display in list
- Add teammate to conversation via # search

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- AI model is available for generating responses

## Test Data

- URL: {{base_url}}
- Test message: Test message for history verification
- Multiple conversation names for testing: multi_1, multi_2, multi_3

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Create a new conversation by clicking the 'Create Conversation' button. Open the newly created conversation. | A fresh conversation opens with no messages. A default AI model is shown in the model selector. |
| 2 | Look at the left sidebar Conversations panel. Verify the newly created conversation appears in the list. | The conversation name is visible in the sidebar list (under 'Today' header). |
| 3 | Click the conversation name in the sidebar to open it. | The conversation opens. The URL updates to include the conversation ID. The message input field is visible. |
| 4 | Click the 'Search conversations' button (magnifying glass icon) in the Conversations panel header. | A search input field appears with a placeholder 'Search conversations...' |
| 5 | Create 2 more conversations. Navigate between them by clicking their names in the sidebar. | Clicking each conversation updates the URL and loads the correct conversation. The message input is visible each time. |
| 6 | In one conversation, type 'Test message for history verification' and send it. Wait for the AI response (up to 30 seconds). | The AI responds. The conversation name in the sidebar updates automatically (it should no longer show 'Naming'). |
| 7 | Create 3 conversations named 'multi_1', 'multi_2', 'multi_3'. Check the sidebar list. | All 3 conversation names are visible in the sidebar Conversations panel. |
| 8 | Look for an 'Add teammate' or 'Add user' button on the conversation page. If found, click it. | If the button exists, a user/teammate picker dialog appears. If not found, the feature is not available on this environment. |

## Expected Final State

If the button exists, a user/teammate picker dialog appears. If not found, the feature is not available on this environment.

## Pass/Fail Criteria

**Pass:**
- New conversation has 0 messages and default model set
- Conversation appears in sidebar after creation
- Click-to-open navigates to correct URL
- Search button opens search input
- Navigation between conversations works
- Sent message generates conversation title
- Multiple conversations all appear in list

**Fail:**
- Conversation missing from sidebar list
- Click does not navigate to conversation URL
- Search input fails to appear
- AI response timeout (> 30s)
- Conversation title stuck on "Naming"
- Multiple conversations not all visible
