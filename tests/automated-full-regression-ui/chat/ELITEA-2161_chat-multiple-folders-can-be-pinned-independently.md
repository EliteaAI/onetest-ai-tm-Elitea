---
id: ELITEA-2161
title: "Chat – Multiple Folders Can Be Pinned Independently"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2161: Chat – Multiple Folders Can Be Pinned Independently

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that multiple folders can be pinned independently and all appear in the pinned folders section.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least two folders exist.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Pin first folder; verify it moves to pinned folders section | First folder pinned |
| 2 | Pin second folder; verify it also moves to pinned folders section | Second folder pinned |
| 3 | Verify both pinned folders appear at top above all unpinned content | Both pinned folders at top |
| 4 | Verify both folders retain their conversations when expanded | Conversations intact |

---

## Expected Final State

Multiple folders pinned independently.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Multiple folders pinned independently.

**Fail:**
- Any step produces an error or unexpected result.
- Only one folder can be pinned at a time.
