---
id: ELITEA-2122
title: "Chat – Folder Rename – Cancel via X Icon Discards Changes"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: tests.ui.chat.test_chat_folder_rename_checkmark_validation.TestChatFolderRenameCheckmarkValidation.test_folder_rename_cancel_via_x_icon_discards_changes
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1539
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2122: Chat – Folder Rename – Cancel via X Icon Discards Changes

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the X icon during folder rename discards the change and restores the original folder name.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one existing folder is present in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| Temp rename | Renamed Folder |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a folder, click three-dot icon, click Edit | Folder name is editable |
| 2 | Clear the current name and type 'Renamed Folder' | New name appears in the input |
| 3 | Click the X (cancel) icon | Input closes without saving |
| 4 | Verify the folder still displays its original name | Original name preserved |

---

## Expected Final State

Original folder name is preserved after cancelling.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cancel preserves original name.

**Fail:**
- Any step produces an error or unexpected result.
- Name is changed despite cancelling.
