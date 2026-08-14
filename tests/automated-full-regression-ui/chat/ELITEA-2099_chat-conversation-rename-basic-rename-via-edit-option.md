---
id: ELITEA-2099
title: "Chat – Conversation Rename – Basic Rename via Edit Option"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: tests.ui.chat.test_conversation_rename_basic_via_edit_option.TestConversationRenameBasicViaEditOption.test_rename_conversation_basic_via_edit_option
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1518
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2099: Chat – Conversation Rename – Basic Rename via Edit Option

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that a conversation can be renamed via the three-dot menu Edit option, and the new name persists after navigating away.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| HI Chat_edited | New conversation name |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Chats section | Conversations list is displayed |
| 2 | Hover over any conversation and verify the three-dot icon appears | Three-dot icon is visible |
| 3 | Click the three-dot icon and verify the context menu shows: Delete, Edit, Move to, Export, Playback, Pin on top | Context menu is visible with all options |
| 4 | Click the Edit option | Conversation name becomes an editable inline input field with current name pre-filled |
| 5 | Verify a checkmark (save) icon and X (cancel) icon appear | Both icons are visible |
| 6 | Clear the current name and type 'HI Chat_edited' | New name appears in the field |
| 7 | Click the checkmark (save) icon | Input closes; conversation displays new name in left panel |
| 8 | Verify no error message is shown | No error shown |
| 9 | Navigate away and return to Chats section | Updated name persists |

---

## Expected Final State

The conversation is renamed and the new name persists after navigation.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Rename succeeds and name persists.

**Fail:**
- Any step produces an error or unexpected result.
- Rename fails, error appears, or name reverts after navigation.
