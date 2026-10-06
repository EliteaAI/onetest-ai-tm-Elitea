---
id: ELITEA-2104
title: "Chat – Conversation Rename – Cannot Paste More Than 50 Characters"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2104: Chat – Conversation Rename – Cannot Paste More Than 50 Characters

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that pasting more than 50 characters into the rename field truncates the input to 50 characters.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| 60-char clipboard string | AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA (60 A's) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name | Field is empty |
| 3 | Paste a 60-character string using Ctrl+V (or Cmd+V on Mac) | Field contains no more than 50 characters; text truncated |
| 4 | Verify 51st and beyond characters are not present | Only 50 characters accepted |
| 5 | Click the checkmark (save) icon | Conversation saved with exactly 50 characters; no error shown |

---

## Expected Final State

Pasted text is truncated to 50 characters; conversation saved successfully.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Paste truncation works; 50-character limit enforced.

**Fail:**
- Any step produces an error or unexpected result.
- More than 50 characters accepted after paste.
