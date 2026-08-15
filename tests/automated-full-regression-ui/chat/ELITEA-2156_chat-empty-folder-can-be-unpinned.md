---
id: ELITEA-2156
title: "Chat – Empty Folder Can Be Unpinned"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_pin_folder.TestUnpinFolderViaContextMenu.test_unpin_empty_folder_retains_empty_state
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1552
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2156: Chat – Empty Folder Can Be Unpinned

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that a pinned empty folder can be unpinned.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pinned empty folder exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a pinned empty folder, click three-dot icon, click 'Unpin' | Folder moves to unpinned section |
| 2 | Verify pin icon is no longer visible | Pin icon removed |
| 3 | Expand the folder and verify it is still empty | Folder shows empty state |

---

## Expected Final State

Empty folder unpinned and still shows empty state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Empty folder unpinned successfully.

**Fail:**
- Any step produces an error or unexpected result.
- Folder cannot be unpinned.
