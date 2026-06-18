---
id: ELITEA-0571
title: "Conversation Creation and List"
priority: high
type: functional
module: conversations
status: ready
execution_type: automated
automation_test_id:
  - test_conversation_management.py:TestCreateConversation.test_create_conversation_via_ui_button
test_conversation_management.py:TestCreateConversation.test_create_conversation_via_api
test_conversation_management.py:TestConversationList.test_conversation_appears_in_list
test_conversation_management.py:TestConversationList.test_click_conversation_to_open
tags: []
requirements: []
---
# ELITEA-0571: Conversation Creation and List

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can create conversations via UI button and API, and that conversations appear in the list and can be opened.

## Preconditions

- User logged into Elitea
- Access to Chat interface

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Click 'New Conversation' button | New conversation created, opens in chat |
| ? | Create conversation via API | Conversation visible in list |
| ? | Click conversation in list | Conversation opens in main area |

## Expected Final State

Conversation opens in main area

## Pass/Fail Criteria

**Pass:**
- Conversation created via UI
- API-created conversation visible
- Click opens conversation
- Conversation list updates

**Fail:**
- Creation fails
- Conversation not in list
- Click doesn't navigate
