---
id: ELITEA-2155
title: "Chat – Empty Folder Can Be Pinned"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_pin_folder.TestPinFolderViaPinOnTop.test_pin_empty_folder_retains_empty_state
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1552
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2155: Chat – Empty Folder Can Be Pinned

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that an empty folder can be pinned and retains its empty state.

---

## Preconditions

- User is logged in to the Elitea platform.
- An empty folder exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over an empty folder, click three-dot icon, click 'Pin on top' | Folder moves to pinned section |
| 2 | Verify pin icon is displayed | Pin icon visible |
| 3 | Expand the pinned folder | Shows 'No conversations added' |

---

## Expected Final State

Empty folder pinned and shows empty state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Empty folder pinned successfully.

**Fail:**
- Any step produces an error or unexpected result.
- Empty folder cannot be pinned or shows error.
