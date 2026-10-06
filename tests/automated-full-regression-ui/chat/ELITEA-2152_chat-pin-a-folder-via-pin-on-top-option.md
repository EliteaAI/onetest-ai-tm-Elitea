---
id: ELITEA-2152
title: "Chat – Pin a Folder via Pin on Top Option"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2152: Chat – Pin a Folder via Pin on Top Option

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that pinning a folder moves it to the top of the panel as a pinned folder with a pin icon.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one unpinned folder exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over an unpinned folder, click three-dot icon, click 'Pin on top' | Folder moves to pinned folders section at top |
| 2 | Verify a pin icon is displayed next to the folder name | Pin icon visible |
| 3 | Verify the folder still shows all its conversations when expanded | Conversations intact |
| 4 | Verify the folder is no longer in its original position | Folder moved from original position |

---

## Expected Final State

Folder pinned and appears at top with pin icon, conversations intact.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Folder pinned; conversations intact.

**Fail:**
- Any step produces an error or unexpected result.
- Folder not pinned or conversations lost.
