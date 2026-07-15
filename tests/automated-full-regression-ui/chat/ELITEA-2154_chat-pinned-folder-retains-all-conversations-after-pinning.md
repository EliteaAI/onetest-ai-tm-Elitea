---
id: ELITEA-2154
title: "Chat – Pinned Folder Retains All Conversations After Pinning"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2154: Chat – Pinned Folder Retains All Conversations After Pinning

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that pinning a folder does not affect its conversations.

---

## Preconditions

- User is logged in to the Elitea platform.
- A folder with multiple conversations exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Expand a folder with multiple conversations and note conversation names | Conversations noted |
| 2 | Hover over the folder, click three-dot icon, click 'Pin on top' | Folder moves to pinned section |
| 3 | Expand the pinned folder | All previous conversations still present |
| 4 | Verify no conversations were lost | All conversations intact |

---

## Expected Final State

All conversations preserved after folder pinning.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All conversations retained after pinning.

**Fail:**
- Any step produces an error or unexpected result.
- Conversations lost after pinning.
