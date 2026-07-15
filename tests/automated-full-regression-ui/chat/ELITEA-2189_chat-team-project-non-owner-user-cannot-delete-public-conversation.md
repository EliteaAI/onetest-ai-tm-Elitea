---
id: ELITEA-2189
title: "Chat – Team Project – Non-Owner User Cannot Delete Public Conversation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2189: Chat – Team Project – Non-Owner User Cannot Delete Public Conversation

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that a non-owner user cannot delete a public conversation owned by another user.

---

## Preconditions

- User is logged in to the Elitea platform.
- Logged in as a non-owner user in a Team project with a public conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Log in as a non-owner user in a Team project | Logged in as non-owner |
| 2 | Navigate to Chats and find a public conversation owned by another user | Public conversation found |
| 3 | Hover over it and click three-dot icon | Context menu appears with limited options |
| 4 | Verify Delete option is disabled or absent | Delete is disabled/absent |
| 5 | Verify only limited options shown (e.g. Playback, Pin on top) | Limited menu shown |

---

## Expected Final State

Non-owner cannot delete public conversation.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Delete disabled for non-owner.

**Fail:**
- Any step produces an error or unexpected result.
- Non-owner can delete public conversation.
