---
id: ELITEA-2160
title: "Chat – Multiple Conversations Can Be Pinned Independently"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2160: Chat – Multiple Conversations Can Be Pinned Independently

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that multiple conversations can be pinned independently and all appear in the pinned section.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least two conversations exist in different date groups.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Pin a conversation from Today; verify it appears in pinned section with pin icon | First conversation pinned |
| 2 | Pin a second conversation from This Week; verify it also appears in pinned section with pin icon | Second conversation pinned |
| 3 | Verify both pinned conversations are visible above unpinned folders | Both pinned; above unpinned content |
| 4 | Verify both conversations are no longer in their original date groups | Removed from date groups |

---

## Expected Final State

Multiple conversations pinned independently and visible in pinned section.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Multiple conversations pinned independently.

**Fail:**
- Any step produces an error or unexpected result.
- Only one conversation can be pinned at a time.
