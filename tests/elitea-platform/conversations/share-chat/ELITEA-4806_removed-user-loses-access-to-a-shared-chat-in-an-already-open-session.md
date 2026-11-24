---
id: ELITEA-4806
title: "Removed user loses access to a shared chat in an already open session"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4806: Removed user loses access to a shared chat in an already open session

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that a user removed from the chat's access loses it in a session where the chat is already open.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- User A owns chat C1 shared with User B.
- User B has C1 open in a separate session and has sent at least 1 message in it.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, remove User B in Share > Team and Save | Toast "Access updated"; the count on the Users card goes down by 1 |
| 2 | As User B, without reload, send a message in C1 | Sending is rejected with a clear access error; no endless spinner |
| 3 | As User B, reload and open the chat list | C1 is not in the list; the direct URL is denied cleanly |
| 4 | As User A, open C1 | Earlier messages of User B are kept; User B is not in the users dropdown |
| 5 | As User A, add User B again and Save | User B can open C1 again with the full history |

---

## Expected Final State

Access removal takes effect for open sessions; history is kept.
