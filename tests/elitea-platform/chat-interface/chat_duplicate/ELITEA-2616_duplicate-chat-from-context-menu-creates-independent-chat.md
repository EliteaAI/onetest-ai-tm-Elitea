---
id: ELITEA-2616
title: "Duplicate Chat from Context Menu Creates Independent Chat"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, context-menu, P0]
requirements: [3837]
---
# ELITEA-2616: Duplicate Chat from Context Menu Creates Independent Chat

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that duplicating a chat from the context menu creates a new independent chat while leaving the original chat unchanged.

## Preconditions

- User is logged in to {{base_url}}
- At least one existing chat with messages and participants exists
- User has permission to duplicate chats

## Test Data

- URL: {{base_url}}
- Existing chat with at least one message and one participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the chat list in the sidebar | Chat list displays with existing chats |
| 2 | Right-click on an existing chat (or click the three-dot menu icon) | Context menu appears with available actions |
| 3 | Locate and click the "Duplicate" option in the context menu | Duplicate action is triggered |
| 4 | Verify a new chat is created in the chat list | New chat appears in the chat list |
| 5 | Open the new duplicated chat | Duplicated chat opens without errors |
| 6 | Verify the original chat still exists in the chat list | Original chat remains unchanged and accessible |
| 7 | Open the original chat and verify all messages are intact | Original chat messages, participants, and settings remain unchanged |

## Expected Final State

- Two independent chats exist: original and duplicate
- Original chat is unchanged (messages, participants, configuration)
- Duplicate chat is created as a new empty conversation with copied participants

## Pass/Fail Criteria

**Pass:**
- Context menu displays Duplicate option
- New chat is created upon selecting Duplicate
- Original chat remains in the list and is unchanged
- Both chats are accessible and independent

**Fail:**
- Duplicate option is missing or disabled
- No new chat is created
- Original chat is modified or deleted
- Error occurs during duplication
