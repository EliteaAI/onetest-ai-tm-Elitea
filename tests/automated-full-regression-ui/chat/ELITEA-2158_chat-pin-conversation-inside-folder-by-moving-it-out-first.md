---
id: ELITEA-2158
title: "Chat – Pin Conversation Inside Folder by Moving It Out First"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_pin_conversation.TestPinDisabledInFolderThenMovedAndPinned.test_pin_disabled_in_folder_then_moved_and_pinned
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1555
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2158: Chat – Pin Conversation Inside Folder by Moving It Out First

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that a conversation moved out of a folder can then be pinned from the general list.

---

## Preconditions

- User is logged in to the Elitea platform.
- A folder with at least one conversation exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Expand a folder and verify 'Pin on top' is greyed out for conversation inside | Pin on top disabled |
| 2 | Click Move to, select 'Back to the list' | Conversation moves to Today |
| 3 | Hover over the conversation in Today, click three-dot icon | Context menu visible |
| 4 | Verify 'Pin on top' is now active and clickable | Pin on top enabled |
| 5 | Click 'Pin on top' | Conversation moves to pinned section with pin icon |

---

## Expected Final State

Conversation moved out of folder and then successfully pinned.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Conversation pinned after moving out of folder.

**Fail:**
- Any step produces an error or unexpected result.
- Pin on top still not available after moving out.
