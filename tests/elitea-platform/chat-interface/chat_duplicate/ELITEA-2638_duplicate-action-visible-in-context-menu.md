---
id: ELITEA-2638
title: "Duplicate Action Visible and Correctly Positioned in Context Menu"
priority: low
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [chat, duplicate, ui, context-menu, P2]
requirements: [3837]
---
# ELITEA-2638: Duplicate Action Visible and Correctly Positioned in Context Menu

**Module:** Chat Interface · **Priority:** Low · **Type:** Functional

**Objective:** Verify that the Duplicate action is visible and correctly positioned in the chat context menu for supported chat types.

## Preconditions

- User is logged in to {{base_url}}
- Multiple chats exist (various types: with users, AI, public, private)
- User has permission to duplicate chats

## Test Data

- URL: {{base_url}}
- Regular chat
- Public chat
- Pinned chat
- Chat with AI participants

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Right-click on a regular chat in chat list | Context menu appears |
| 2 | Verify "Duplicate" option is visible | Duplicate option present |
| 3 | Verify position in menu (e.g., after "Rename", before "Delete") | Logical placement in menu |
| 4 | Close context menu | Menu closes |
| 5 | Click three-dot menu icon on same chat | Context menu appears |
| 6 | Verify "Duplicate" option also visible via three-dot menu | Duplicate option present |
| 7 | Test on public chat | Duplicate option available |
| 8 | Test on pinned chat | Duplicate option available |
| 9 | Test on chat with AI participants | Duplicate option available |
| 10 | Verify Duplicate option is enabled (not grayed out) | Option is clickable |

## Expected Final State

- Duplicate option visible in context menu
- Available via both right-click and three-dot menu
- Correctly positioned among other actions
- Enabled for all supported chat types

## Pass/Fail Criteria

**Pass:**
- Duplicate option visible in context menu
- Available for all supported chat types
- Logical menu positioning
- Enabled and clickable
- Consistent across access methods

**Fail:**
- Duplicate option missing
- Grayed out or disabled
- Inconsistent positioning
- Not available for some chat types
- UI inconsistency between access methods
