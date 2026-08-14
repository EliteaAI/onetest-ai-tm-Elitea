---
id: ELITEA-2102
title: "Chat – Conversation Rename – Save with 50 Characters (Boundary)"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_conversation_rename_length_boundaries.TestConversationRenameLengthBoundaries.test_rename_conversation_length_boundary[ELITEA-2102-50-chars]"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1518
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2102: Chat – Conversation Rename – Save with 50 Characters (Boundary)

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that exactly 50 characters is the boundary limit accepted and saved for a conversation name.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| 50-char string | AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA (50 A's) |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a conversation, click three-dot icon, click Edit | Conversation name is editable |
| 2 | Clear the current name and type exactly 50 characters | All 50 characters are accepted |
| 3 | Click the checkmark (save) icon | Conversation is renamed with 50-character name |
| 4 | Verify no error message is shown | Save completes successfully |

---

## Expected Final State

Conversation is renamed with a 50-character name (boundary value) without errors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- 50-character name is accepted and saved.

**Fail:**
- Any step produces an error or unexpected result.
- Name is rejected at boundary or error is shown.
