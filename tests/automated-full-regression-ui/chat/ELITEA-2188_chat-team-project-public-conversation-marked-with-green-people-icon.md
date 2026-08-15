---
id: ELITEA-2188
title: "Chat – Team Project – Public Conversation Marked with Green People Icon in Chat List"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_public_conversation_green_icon.TestPublicConversationGreenIcon.test_public_conversation_shows_green_icon_in_chat_list
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1566
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2188: Chat – Team Project – Public Conversation Marked with Green People Icon in Chat List

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that public conversations in Team projects show a green multi-user icon and full conversation history is accessible.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Team project with at least one public conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats in Team project | Conversations listed |
| 2 | Locate a public conversation; verify green people icon displayed next to name | Green icon visible |
| 3 | Verify private conversations do NOT show the green icon | Private convs without green icon |
| 4 | Click the public conversation | Full history shown; all messages with senders and timestamps |
| 5 | Verify message input field available; PARTICIPANTS USERS section shows participants | Input field and PARTICIPANTS visible |

---

## Expected Final State

Public conversations show green icon; history and input available.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Public conv has green icon; history accessible.

**Fail:**
- Any step produces an error or unexpected result.
- Green icon missing or history not accessible.
