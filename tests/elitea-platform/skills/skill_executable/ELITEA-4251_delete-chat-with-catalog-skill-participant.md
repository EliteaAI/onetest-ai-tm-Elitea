---
id: ELITEA-4251
title: Delete chat with Catalog skill participant
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, catalog, chat, deletion, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4251: Delete chat with Catalog skill participant

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that chat with Catalog skill participant can be deleted like any other chat.

**Coverage:**
- Chat can be deleted
- Deletion confirmation prompt
- Chat removed from Chats list
- Skill participant relationship removed

## Preconditions

- User is logged in to {{base_url}}
- Chat with Catalog skill participant exists in Chats list
- User has permission to delete chats

## Test Data

- Existing chat with Catalog skill participant
- Expected: Chat deleted successfully

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chats list in left sidebar | Chats list displays with chat containing Catalog skill |
| 2 | Locate the chat with Catalog skill participant | Chat visible in the list |
| 3 | Hover over the chat item | Actions appear (e.g., 3-dot menu) |
| 4 | Click the 3-dot menu or delete icon on the chat | Dropdown menu or actions appear |
| 5 | Click "Delete" action | Deletion confirmation dialog appears |
| 6 | Read the confirmation message | Message warns about deleting the chat (e.g., "Are you sure you want to delete this chat?") |
| 7 | Click "Confirm" or "Delete" to proceed | Deletion is confirmed |
| 8 | Observe the Chats list | Chat is removed from the Chats list |
| 9 | Verify chat no longer appears | Deleted chat is not visible in any view |
| 10 | (Optional) Try to navigate to deleted chat via direct URL | Chat is not accessible, shows error or redirects |
| 11 | Verify skill participant relationship is removed | Chat data including skill participant is deleted |

## Expected Final State

Chat deleted successfully; removed from Chats list; skill participant relationship removed; chat data deleted.

## Pass/Fail Criteria

**Pass:** Chat deleted after confirmation, removed from list, no longer accessible, data properly cleaned up.

**Fail:** Chat not deleted, still appears in list, or deletion fails.
