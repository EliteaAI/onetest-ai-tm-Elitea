---
id: ELITEA-2100
title: "Chat – Conversation Rename – Cancel Discards Changes"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: tests.ui.chat.test_conversation_rename_cancel_discards_changes.TestConversationRenameCancelDiscardsChanges.test_rename_conversation_cancel_discards_changes
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1518
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2100: Chat – Conversation Rename – Cancel Discards Changes

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the X (cancel) icon during rename discards the change and the original name is preserved.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Renamed Chat | Temporary new name typed |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Chats section | Conversations list is displayed |
| 2 | Hover over any conversation, click three-dot icon, click Edit | Conversation name is editable with checkmark and X icons |
| 3 | Clear the current name and type 'Renamed Chat' | New name appears in the field |
| 4 | Click the X (cancel) icon | Input field closes without saving |
| 5 | Verify the conversation still displays its original name | Original name is preserved |
| 6 | Verify no changes were applied | Conversation name unchanged |

---

## Expected Final State

The original name is preserved after cancelling the rename.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Original name preserved after cancel.

**Fail:**
- Any step produces an error or unexpected result.
- Name is changed despite cancelling.
