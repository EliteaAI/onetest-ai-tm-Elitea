---
id: ELITEA-2098
title: "Open Existing Conversation from a Folder"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2098: Open Existing Conversation from a Folder

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that folders can be expanded to list their conversations, and that clicking a conversation inside a folder opens it correctly and highlights the active conversation.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one folder with conversations exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to the Chats page and locate a folder | Folder is shown with a folder icon |
| 2 | Click the folder to expand it | All conversations stored inside the folder are listed |
| 3 | Click on a conversation inside the folder | Conversation content is displayed with full message history |
| 4 | Verify the message input field at the bottom is active | Input field is active |
| 5 | Verify the correct model or agent name is shown in the input bar | Model/agent name visible |
| 6 | Verify the PARTICIPANTS panel shows the correct participant | PARTICIPANTS shows correct participant |
| 7 | Verify the conversation entry in the folder list is highlighted | Active conversation is highlighted |
| 8 | Click on a different conversation inside the same folder | Interaction window updates to the new conversation; previous is no longer highlighted |

---

## Expected Final State

Folder expands correctly, conversations inside open with full history, and active conversation is visually highlighted.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Folder expands; conversations open correctly; active conversation is highlighted.

**Fail:**
- Any step produces an error or unexpected result.
- Folder does not expand or conversation does not load.
