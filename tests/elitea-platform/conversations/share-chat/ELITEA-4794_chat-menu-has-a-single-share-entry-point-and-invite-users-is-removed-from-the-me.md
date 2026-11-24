---
id: ELITEA-4794
title: "Chat menu has a single Share entry point and Invite Users is removed from the + menu"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4794: Chat menu has a single Share entry point and Invite Users is removed from the + menu

**Module:** conversations · **Priority:** critical · **Type:** functional

**Objective:** Verify that the chat menu has one "Share" item instead of Make public, Restrict access, Share and Share externally, that it opens the Share Chat window for the owner and copies the link for everyone else, that it is hidden in the Public project, and that Invite Users is removed from the "+" menu of the message input.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project with at least 2 members: User A (owner) and User B.
- User A owns chat C1; User A owns chat C2 shared with User B.
- User A has a chat in the personal project.
- Access to the Public project.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open the "⋮" menu of C1 in the chat list | One "Share" item. No Make public, Restrict access, Share externally or Manage links. Rename, Move to, Playback, Duplicate, Export, Pin on top and Delete are still there |
| 2 | Click Share | The Share Chat window opens: title "Share Chat", the chat name under it, tabs Team and Externally |
| 3 | Close the window and click "+" in the message input | Attach Files, Modules, Agents, Pipelines, Skills, Toolkits, MCPs. No Invite Users |
| 4 | As User B, open the "⋮" menu of C2 and click Share | No window opens. The chat link is copied; toast "Link copied. Only people with access can open it." |
| 5 | As User A, open Share on the chat in the personal project | The window opens without tabs and shows the Externally content |
| 6 | Switch to the Public project and open the "⋮" menu of a chat | No Share item. No access_denied requests in DevTools > Network |
| 7 | As User A, use Rename, Duplicate and Export on C1 | Each action works as before |

---

## Expected Final State

Sharing is reached through one "Share" item; the removed items and Invite Users are gone everywhere.

---

## Notes

- Public project: #7651 (fixed).
- Invite Users in the "+" menu: #7654.
