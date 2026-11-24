---
id: ELITEA-4803
title: "Whole team access mentions and notifications for people who have not joined the chat"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, access-control, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4803: Whole team access mentions and notifications for people who have not joined the chat

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that people who get access through Whole team but have never opened the chat are notified, listed in the "@" selector and can be mentioned.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Team project; User A owns chat C1 shared with User B only.
- User D is a project member who has never opened C1. Separate sessions for User B and User D.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, share C1 with Whole team and Save | The Users card shows "Whole Team (N)" |
| 2 | As User D, open Notifications | User D got "<User A> added you to <C1>" |
| 3 | As User A, type "@" in the message input | The selector lists all teammates except User A, and Everyone; typing filters it |
| 4 | Mention User D (from "@" or from the Users dropdown) and send | The message is sent without errors; User D becomes a participant and gets a mention notification that opens C1 |
| 5 | Send "@Everyone hi" | Everyone with access is notified, not only the existing participants |

---

## Expected Final State

Whole team access behaves like explicit access for mentions and notifications.

---

## Notes

- Depends on #7680 (step 2) and #7718 (step 3); server part #7523.
