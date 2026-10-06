---
id: ELITEA-2157
title: "Chat – Conversation Inside a Folder Cannot Be Pinned Separately"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2157: Chat – Conversation Inside a Folder Cannot Be Pinned Separately

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the 'Pin on top' option is greyed out for conversations inside folders.

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
| 1 | Navigate to Chats, expand a folder, hover over a conversation inside, click three-dot icon | Context menu visible |
| 2 | Verify 'Pin on top' option is greyed out / disabled | Pin on top is disabled |
| 3 | Attempt to click the greyed out Pin on top option | Click has no effect |
| 4 | Verify the conversation is not pinned and remains inside the folder | Conversation stays in folder |

---

## Expected Final State

Conversations inside folders cannot be pinned directly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pin on top disabled for conversations inside folders.

**Fail:**
- Any step produces an error or unexpected result.
- Pin on top works for conversations inside folders.
