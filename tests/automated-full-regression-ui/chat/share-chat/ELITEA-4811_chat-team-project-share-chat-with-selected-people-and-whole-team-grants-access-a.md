---
id: ELITEA-4811
title: "Chat – Team Project – Share Chat with Selected People and Whole Team Grants Access and Removing Access Revokes It"
priority: critical
type: functional
module: conversations
status: draft
execution_type: manual
tags: [manual:UI:regression, feat:chat, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4811: Chat – Team Project – Share Chat with Selected People and Whole Team Grants Access and Removing Access Revokes It

**Module:** conversations · **Priority:** critical · **Type:** functional

**Objective:** Verify the main team-sharing journey: the owner shares a chat with selected people and with the whole team, access really works, and removing access takes it away.

---

## Preconditions

- User is logged in to the Elitea platform.
- Team project with at least 3 members: User A (owner), User B, User C, each with a separate session.
- User A owns chat C1 with at least 1 message; only the owner has access.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open the "⋮" menu of C1 and click Share | The Share Chat window opens on Team; "People with access – 1"; User A with the badge "Owner" |
| 2 | Add User B through the search and click Save | Toast "Access updated"; User B is listed; the Users card shows "2 users" |
| 3 | As User B, open C1 from the chat list and by URL | C1 opens with the full history; User B can send a message |
| 4 | As User C, open the URL of C1 | Access is denied; C1 is not in User C's list |
| 5 | As User A, pick Whole team and Save | The Users card shows "Whole Team (N)", N = all project members |
| 6 | As User C, open C1 | C1 opens |
| 7 | As User A, click "Remove access for all" and Save | Only the owner is left; the Users card shows a lock and "Only You" |
| 8 | As User B and User C, reload C1 | Access is denied for both; C1 is not in their lists; User A keeps full access |

---

## Expected Final State

Chat access always matches what the owner saved in the Share Chat window.
