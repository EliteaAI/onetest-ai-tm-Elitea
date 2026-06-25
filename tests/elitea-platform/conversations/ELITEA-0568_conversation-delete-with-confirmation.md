---
id: ELITEA-0568
title: "Conversation Delete with Confirmation"
priority: high
type: functional
module: conversations
status: ready
execution_type: automated
automation_test_id:
  - test_conversation_management.py:TestConversationActions.test_delete_conversation_with_confirmation
  - test_conversation_management.py:TestConversationActions.test_delete_conversation_cancel
  - test_conversation_management.py:TestConversationActions.test_delete_conversation_and_verify_ui
tags: []
requirements: []
---
# ELITEA-0568: Conversation Delete with Confirmation

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify conversation deletion flow with confirmation dialog and cancel option.

**Coverage:**
- Delete conversation shows confirmation dialog
- Cancel button preserves conversation
- Confirm button deletes conversation
- Deleted conversation removed from UI list

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- At least one conversation exists (create manually if needed)
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Conversation names for testing: del_confirm, del_cancel, del_me

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Create a new conversation (e.g., named 'del_confirm'). Verify it appears in the sidebar Conversations list. | Conversation is visible in the sidebar list. |
| 2 | Hover over the conversation in the sidebar. Click the three-dot menu icon that appears, then click 'Delete'. | A confirmation dialog appears with the title 'Delete conversation' (or similar). |
| 3 | Verify the dialog has 'Cancel' and 'Delete' buttons. Click 'Delete' to confirm. | The dialog closes. The conversation disappears from the sidebar list within a few seconds. |
| 4 | Refresh the page and verify the deleted conversation is no longer in the sidebar list. | The conversation is gone from the list after refresh. |
| 5 | Create another conversation (e.g., 'del_cancel'). Open the delete dialog the same way, but this time click 'Cancel'. | The dialog closes. The conversation remains in the sidebar list. |
| 6 | Create a third conversation (e.g., 'del_me'). Verify it appears in the sidebar. Then delete it using any method. Reload the page. | After reload, the conversation no longer appears in the sidebar list. |

## Expected Final State

After reload, the conversation no longer appears in the sidebar list.

## Pass/Fail Criteria

**Pass:**
- Delete confirmation dialog appears with correct title
- Confirm deletes conversation from sidebar and API
- Cancel preserves conversation (still in list)
- API deletion reflects in UI after reload

**Fail:**
- Delete dialog fails to appear
- Conversation remains in list after confirm
- Cancel accidentally deletes conversation
- API confirms deletion but UI still shows conversation
