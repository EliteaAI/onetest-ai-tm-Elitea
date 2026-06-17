---
id: ELITEA-0567
title: "Conversation Fixture Data Lifecycle"
priority: medium
type: functional
module: conversations
status: ready
execution_type: automated
automation_test_id:
  - test_conversation_management.py:TestConversationIsolation.test_fixture_creates_fresh_conversation
test_conversation_management.py:TestConversationIsolation.test_fixture_cleanup_cycle
tags: []
requirements: []
---
# ELITEA-0567: Conversation Fixture Data Lifecycle

**Module:** Conversations · **Priority:** Medium · **Type:** Functional

**Objective:** Verify pytest fixture behavior for conversation test data: fresh creation and cleanup.

**Coverage:**
- Fixture creates fresh conversation for each test
- Fixture cleanup cycle (create → use → delete)

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Conversation name for testing: autotest_cleanup

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar. Create a new conversation by clicking the 'Create Conversation' button. | A new conversation is created with a valid ID and appears in the sidebar Conversations list. |
| 2 | Click on the newly created conversation in the sidebar to open it. | The conversation opens. The URL contains the conversation ID. The message input is visible. |
| 3 | Verify the conversation has no messages (it should be a fresh, empty conversation). | The conversation shows 0 messages. No stale data from previous sessions. |
| 4 | Create another conversation (you can rename it to 'autotest_cleanup' if the UI allows). | The new conversation is created successfully. |
| 5 | Verify the 'autotest_cleanup' conversation appears in the sidebar Conversations list. | The conversation name is visible in the sidebar. |
| 6 | Delete the 'autotest_cleanup' conversation (via the three-dot menu > Delete > Confirm). Verify it disappears from the sidebar. | The conversation is removed from the sidebar list after deletion. |

## Expected Final State

The conversation is removed from the sidebar list after deletion.

## Pass/Fail Criteria

**Pass:**
- Fixture creates fresh conversation per test
- Conversation loads with 0 messages (no stale data)
- Create → list → delete → verify cycle completes cleanly
- No orphaned conversations after cleanup

**Fail:**
- Fixture fails to create conversation
- Stale messages found in new conversation
- Delete doesn't remove conversation from API list
- Orphaned conversations left in system
