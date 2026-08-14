---
id: ELITEA-2103
title: "Chat – Conversation Rename – Cannot Type Beyond 50 Characters"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: tests.ui.chat.test_conversation_rename_length_boundaries.TestConversationRenameLengthBoundaries.test_rename_conversation_type_beyond_max_length_truncates
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1518
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2103: Chat – Conversation Rename – Cannot Type Beyond 50 Characters

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that the rename input field enforces a 50-character maximum and does not accept a 51st character.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| 51+ characters | 51-character string |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and attempt to type 51 characters | Only first 50 characters are accepted; 51st is not entered |
| 3 | Verify the character count does not exceed 50 | Max 50 characters enforced |
| 4 | Click the checkmark (save) icon | Conversation saved with exactly 50 characters; no error shown |

---

## Expected Final State

The input enforces a 50-character maximum; the 51st character is not accepted.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- 50-character limit is enforced.

**Fail:**
- Any step produces an error or unexpected result.
- 51 characters are accepted or an error appears.
