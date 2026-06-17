---
id: ELITEA-0570
title: "Conversation Rename and Delete"
priority: high
type: functional
module: conversations
status: ready
execution_type: automated
automation_test_id:
  - test_conversation_management.py:TestConversationActions.test_rename_conversation_via_ui
test_conversation_management.py:TestConversationActions.test_conversation_api_rename
test_conversation_management.py:TestConversationActions.test_delete_conversation_with_confirmation
test_conversation_management.py:TestConversationActions.test_delete_conversation_and_verify_ui
tags: []
requirements: []
---
# ELITEA-0570: Conversation Rename and Delete

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can rename and delete conversations via UI and API, with proper confirmation flows.

## Preconditions

- User logged into Elitea
- Test conversation exists

## Test Data

- URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Open conversation actions menu | Menu shows Rename, Delete options |
| ? | Click Rename, enter new title | Title updated in list |
| ? | Click Delete | Confirmation dialog appears |
| ? | Confirm deletion | Conversation removed from list |

## Expected Final State

Conversation removed from list

## Pass/Fail Criteria

**Pass:**
- Rename via UI updates title
- API rename reflects in UI
- Delete requires confirmation
- Deleted conversation removed

**Fail:**
- Rename doesn't persist
- Delete without confirmation
- Deleted still visible
