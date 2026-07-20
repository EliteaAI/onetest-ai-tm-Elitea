---
id: ELITEA-2090
title: "Create New Conversation from Private Project via +Chat with default LLM"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id: tests.ui.chat.test_conversation_management.TestCreateConversation.test_create_conversation_via_ui_button
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/682
---

# ELITEA-2090: Create New Conversation from Private Project via +Chat with default LLM

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking +Chat in a Private project opens a new blank conversation, the default LLM is pre-selected, and after sending the first message the conversation is auto-named.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Private project.

---

## Test Data

| Field | Value |
|-------|-------|
| First message | Generate test cases for login functionality |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Private project and go to the Chats page | Chats page is displayed |
| 2 | Click the + Chat button in the left sidebar | A new blank conversation opens showing greeting screen and + Chat button becomes inactive |
| 3 | Type "Generate test cases for login functionality" in the input field | Message is entered |
| 4 | Observe the model selector — verify the default LLM is pre-selected | Default LLM shown (e.g. "GPT-5.2") |
| 5 | Click the Send button | A new entry appears in the "Today" dropdown with a "Naming…" placeholder spinner |
| 6 | Wait for naming to complete | Conversation is auto-named based on first message; spinner disappears; + Chat button becomes active; LLM response is rendered |

---

## Expected Final State

A new conversation is created, auto-named based on the first message, and the LLM responds successfully.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Conversation opens, message is sent, auto-naming completes, LLM responds.

**Fail:**
- Any step produces an error or unexpected result.
- Conversation is not created or auto-naming fails.
