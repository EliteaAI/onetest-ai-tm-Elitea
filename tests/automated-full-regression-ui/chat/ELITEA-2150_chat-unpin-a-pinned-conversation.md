---
id: ELITEA-2150
title: "Chat – Unpin a Pinned Conversation"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_pin_conversation.TestUnpinConversationViaContextMenu.test_unpin_conversation_via_context_menu
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1552
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2150: Chat – Unpin a Pinned Conversation

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that unpinning a pinned conversation removes it from the pinned section and returns it to the appropriate date group.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one pinned conversation exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats, hover over a pinned conversation, click three-dot icon, click 'Unpin' | Conversation removed from pinned section |
| 2 | Verify the pin icon is no longer displayed | Pin icon gone |
| 3 | Verify the conversation reappears in the appropriate date group | Conversation in correct date group |

---

## Expected Final State

Conversation unpinned and returned to date group.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Conversation unpinned and in correct date group.

**Fail:**
- Any step produces an error or unexpected result.
- Conversation remains pinned or disappears.
