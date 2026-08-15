---
id: ELITEA-2159
title: "Chat – Left Panel Order Verified After Multiple Pin Actions"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_pin_conversation.TestChatPanelOrderingPinnedFoldersAndConversations.test_pinned_folder_and_conversation_render_above_unpinned_panel_order
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1555
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2159: Chat – Left Panel Order Verified After Multiple Pin Actions

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify the left panel maintains correct ordering after pinning both a folder and a conversation.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one folder and one ungrouped conversation exist.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Pin at least one folder using 'Pin on top' | Folder in pinned folders section |
| 2 | Pin at least one conversation (not inside a folder) using 'Pin on top' | Conversation in pinned conversations section |
| 3 | Verify panel order: pinned folders (pin icon), pinned conversations (pin icon), unpinned folders, unpinned conversations by Today/This Week/Older | Panel order correct |
| 4 | Verify no unpinned item appears above a pinned item of the same type | Ordering maintained |
| 5 | Verify no pinned conversation appears above pinned folders | Folders before conversations in pinned area |

---

## Expected Final State

Panel order maintained correctly after multiple pin actions.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Panel order correct after multiple pins.

**Fail:**
- Any step produces an error or unexpected result.
- Panel order is incorrect after pinning.
