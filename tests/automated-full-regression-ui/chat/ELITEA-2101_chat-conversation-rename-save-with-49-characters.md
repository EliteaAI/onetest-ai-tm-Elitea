---
id: ELITEA-2101
title: "Chat – Conversation Rename – Save with 49 Characters"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2101: Chat – Conversation Rename – Save with 49 Characters

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that a 49-character name is accepted and saved successfully for a conversation.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| 49-char string | AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA (49 A's) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and type exactly 49 characters | All 49 characters are accepted |
| 3 | Click the checkmark (save) icon | Conversation is renamed with 49-character name |
| 4 | Verify no error message is shown | Save completes successfully |

---

## Expected Final State

Conversation is renamed with a 49-character name without errors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- 49-character name is accepted and saved.

**Fail:**
- Any step produces an error or unexpected result.
- Name is rejected or error is shown.
