---
id: ELITEA-2757
title: "Chat – Create new conversation from folder context menu"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6]
requirements: [EliteaAI/elitea_issues#1604]
---

# ELITEA-2757: Chat – Create new conversation from folder context menu

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Verify that a user can create a new conversation directly inside a folder using the "New chat" option in folder context menu, and the conversation is properly saved in that folder.

---

## Preconditions

- User is logged in to `{{base_url}}`
- User is on the Chats section
- At least one folder exists in the Chats section

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test message | Explain the concept of machine learning |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Chats section and click three-dot icon (⋮) on the folder row | Context menu appears with options: **New chat**, Rename, Pin on top, Delete |
| 2 | Click "New chat" in the context menu | New blank conversation opens in the main chat area; folder auto-expands if collapsed |
| 3 | Verify the default LLM is pre-selected in the model selector | Default project LLM is displayed (e.g., Anthropic Sonnet 5) |
| 4 | Send message: "Explain the concept of machine learning" | Message is sent; "Naming…" spinner appears next to conversation entry in the folder |
| 5 | Wait for auto-naming to complete | Conversation is auto-named based on message content; spinner disappears |
| 6 | Verify conversation appears inside the target folder, NOT in Today/This Week/Older sections | Conversation is visible only in the folder's conversation list |
| 7 | Collapse and re-expand the folder | Conversation remains visible in the folder |
| 8 | Refresh the page (F5) and navigate back to Chats section | After reload, conversation is still present in the folder with name and content intact |

---

## Expected Final State

- "New chat" option is available in folder context menu (both right-click and three-dot)
- Conversation is created inside the folder, not in root date-based sections
- Default LLM is pre-selected, auto-naming works correctly
- Conversation persists after page refresh

---

## Pass/Fail Criteria

**Pass:**
- "New chat" option appears in folder context menu
- Conversation is created inside the target folder
- Conversation does NOT appear in Today/This Week/Older sections
- Auto-naming completes successfully
- Conversation persists after page refresh

**Fail:**
- "New chat" option is missing from context menu
- Conversation appears in root list instead of folder
- Conversation appears in both folder and date-based sections
- Conversation is lost after page refresh
