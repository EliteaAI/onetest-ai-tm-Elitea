---
id: ELITEA-2106
title: "Chat – Conversation Rename – Check Icon Inactive When Name Field is Empty"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_conversation_rename_checkmark_active_state.TestConversationRenameCheckmarkActiveState.test_rename_checkmark_inactive_click_has_no_effect[ELITEA-2106-empty-field]"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1522
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2106: Chat – Conversation Rename – Check Icon Inactive When Name Field is Empty

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the checkmark (save) icon is disabled when the conversation name field is cleared to empty.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the entire content of the input field | Field is empty |
| 3 | Verify the checkmark icon is displayed in a disabled/inactive state (greyed out) | Checkmark is inactive |
| 4 | Attempt to click the checkmark icon | Click has no effect; save is not triggered |
| 5 | Verify the input field remains open and conversation name is not changed | Field stays open; name unchanged |

---

## Expected Final State

The checkmark icon is disabled when the field is empty; save cannot be triggered.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Checkmark inactive when field is empty.

**Fail:**
- Any step produces an error or unexpected result.
- Save is triggered with empty field.
