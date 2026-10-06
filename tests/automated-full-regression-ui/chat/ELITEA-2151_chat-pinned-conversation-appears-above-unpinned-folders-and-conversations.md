---
id: ELITEA-2151
title: "Chat – Pinned Conversation Appears Above Unpinned Folders and Conversations"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2151: Chat – Pinned Conversation Appears Above Unpinned Folders and Conversations

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify the left panel ordering: pinned folders, pinned conversations, unpinned folders, unpinned conversations.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one pinned and one unpinned item exist.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Pin at least one conversation using Pin on top | Conversation appears in pinned section |
| 2 | Verify left panel order from top to bottom: pinned folders, pinned conversations, unpinned folders, unpinned conversations by Today/This Week/Older | Panel order matches expected |
| 3 | Verify no pinned item appears below any unpinned item | Ordering is correct |

---

## Expected Final State

Panel maintains correct ordering with pinned items above unpinned.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Panel order is: pinned folders, pinned conversations, unpinned folders, unpinned conversations.

**Fail:**
- Any step produces an error or unexpected result.
- Panel order is incorrect.
