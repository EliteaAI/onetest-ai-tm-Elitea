---
id: ELITEA-4813
title: "Chat – Team Project – Shared Chat for a User Who Is Not the Owner Allows Copy Link Only"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [manual:UI:regression, feat:chat, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4813: Chat – Team Project – Shared Chat for a User Who Is Not the Owner Allows Copy Link Only

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that a user who is not the owner can use a shared chat, that every Share entry point only copies the link, and that access cannot be managed by this user.

---

## Preconditions

- User is logged in to the Elitea platform.
- Team project; User A owns chat C1 shared with User B (selected people) and has at least 1 active external link on it.
- User B is logged in and has access to the Public project.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User B, open C1 and send a message | The message is sent; the Users card shows "N users" without a "🔗" count |
| 2 | Open the "⋮" menu of C1 | One "Share" item; no Make public, Restrict access or Share externally |
| 3 | Click Share | No window opens; the link is copied; toast "Link copied. Only people with access can open it." |
| 4 | Hover the Users card and click its Share icon | Same as step 3 |
| 5 | Collapse the Participants panel, open the users dropdown and click Share | No window opens; the link is copied with the same toast |
| 6 | Click "+" in the message input | No Invite Users |
| 7 | Switch to the Public project and open the "⋮" menu of a chat | No Share item |

---

## Expected Final State

Users who are not the owner can work in the chat and copy its link but cannot manage access or see external links.
