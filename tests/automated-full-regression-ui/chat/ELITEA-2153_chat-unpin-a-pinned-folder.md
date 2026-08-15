---
id: ELITEA-2153
title: "Chat – Unpin a Pinned Folder"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_pin_folder.TestUnpinFolderViaContextMenu.test_unpin_folder_via_context_menu
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1552
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2153: Chat – Unpin a Pinned Folder

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that unpinning a pinned folder moves it back to the unpinned folder section.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one pinned folder exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a pinned folder, click three-dot icon, click 'Unpin' | Folder removed from pinned section |
| 2 | Verify the pin icon is no longer visible | Pin icon removed |
| 3 | Verify the folder reappears in the unpinned folders section | Folder in unpinned section |
| 4 | Verify the folder retains all its conversations | Conversations intact |

---

## Expected Final State

Folder unpinned and in unpinned section, conversations intact.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Folder unpinned; conversations intact.

**Fail:**
- Any step produces an error or unexpected result.
- Folder remains pinned or conversations lost.
