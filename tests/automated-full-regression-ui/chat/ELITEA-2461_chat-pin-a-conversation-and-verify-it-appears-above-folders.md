---
id: ELITEA-2461
title: "Chat – Pin a conversation and verify it appears above folders and date groups"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_pin_conversation.TestPinConversationViaPinOnTop.test_pin_conversation_via_pin_on_top
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1555
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2461: Chat – Pin a conversation and verify it appears above folders and date groups

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Chat – Pin a conversation and verify it appears above folders and date groups. Success is confirmed when verify the overall left panel order is: pinned folders at top, then pinned conversations, then unpinned folders, then unpinned conversations grouped by today/this week/older.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Chats section and hover over any conversation in Today, This Week, or Older | Target page/section loads successfully. |
| 2 | Click the three-dot icon and click Pin on top | Control responds; expected next state is shown. |
| 3 | Verify the conversation moves out of its original date group and appears in the pinned conversations section | Condition holds as described. |
| 4 | Verify a pin icon is displayed next to the pinned conversation name | Condition holds as described. |
| 5 | Verify the overall left panel order is: pinned folders at top, then pinned conversations, then unpinned folders, then unpinned conversations grouped by Today/This Week/Older | Condition holds as described. |

---

## Expected Final State

Verify the overall left panel order is: pinned folders at top, then pinned conversations, then unpinned folders, then unpinned conversations grouped by Today/This Week/Older.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Chat – Pin a conversation and verify it appears above folders and date groups.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
