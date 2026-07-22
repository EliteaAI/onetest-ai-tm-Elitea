---
id: ELITEA-2132
title: "Chat – Folder Creation via CHATS Header Icon"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id: tests.ui.chat.test_folder_creation.TestChatFolderCreation.test_create_folder_via_chats_header_icon
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/698
---

# ELITEA-2132: Chat – Folder Creation via CHATS Header Icon

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that clicking the folder icon in the CHATS header creates a new folder with the default name and the folder appears correctly in the panel.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is on the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Chats section | Chats section is displayed |
| 2 | Verify CHATS panel header displays a folder icon next to the search icon | Folder icon visible |
| 3 | Click the folder icon in the CHATS header | New folder entry appears at top of folder list in editable mode with default name e.g. 'New folder' |
| 4 | Verify checkmark and X icons are displayed next to the input field | Both icons visible |
| 5 | Click the checkmark icon without changing the default name | Folder created with default name; appears in folder list |
| 6 | Verify the folder displays a folder icon and expand arrow | Folder visible in panel |
| 7 | Verify the folder shows empty state when expanded | Folder is empty or shows 'No conversations added' |

---

## Expected Final State

Folder created with default name and is empty.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Folder created with default name.

**Fail:**
- Any step produces an error or unexpected result.
- Folder not created or shows unexpected content.
