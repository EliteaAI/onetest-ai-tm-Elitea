---
id: ELITEA-2754
title: "Chat – New chat from folder works in Private and Team projects"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.6]
requirements: [EliteaAI/elitea_issues#1604]
---

# ELITEA-2754: Chat – New chat from folder works in Private and Team projects

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Verify that creating a conversation via "New chat" option in folder context menu works consistently in both Private and Team projects.

---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to both a Private project and a Team project
- Both projects have at least one folder in the Chats section

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Private project message | Test message in Private project |
| Team project message | Test message in Team project |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Select the Private project and go to Chats section | Private project is active, Chats section displayed |
| 2 | Click three-dot icon (⋮) on the folder row → click "New chat" | New blank conversation opens |
| 3 | Send message: "Test message in Private project" | Message is sent; conversation is auto-named and appears in the folder |
| 4 | Switch to the Team project and go to Chats section | Team project is active, Chats section displayed |
| 5 | Click three-dot icon (⋮) on the folder row → click "New chat" | New blank conversation opens |
| 6 | Send message: "Test message in Team project" | Message is sent; conversation is auto-named and appears in the folder |
| 7 | Switch back to Private project → expand the folder | First conversation is still present in Private project folder |
| 8 | Verify conversations are isolated to their respective projects | Each conversation exists only in its project's folder |

---

## Expected Final State

- "New chat" from folder works identically in Private and Team projects
- Conversations are properly isolated to their respective projects

---

## Pass/Fail Criteria

**Pass:**
- Conversation creation works in Private project folder
- Conversation creation works in Team project folder
- Conversations are properly isolated to their respective projects

**Fail:**
- Conversation creation fails in either project type
- Behavior is inconsistent between project types
- Conversations appear in wrong project
