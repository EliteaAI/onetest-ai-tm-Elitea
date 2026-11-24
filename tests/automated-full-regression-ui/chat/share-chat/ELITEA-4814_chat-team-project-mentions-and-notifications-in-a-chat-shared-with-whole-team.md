---
id: ELITEA-4814
title: "Chat – Team Project – Mentions and Notifications in a Chat Shared with Whole Team"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [manual:UI:regression, feat:chat, share-chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-4814: Chat – Team Project – Mentions and Notifications in a Chat Shared with Whole Team

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that sharing a chat with the whole team notifies the teammates and that people who have not joined yet can be mentioned and notified.

---

## Preconditions

- User is logged in to the Elitea platform.
- Team project; User A owns chat C1 shared with User B only.
- User D is a project member who has never opened C1. User A, User B and User D have separate sessions.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, share C1 with Whole team and Save | The Users card shows "Whole Team (N)" |
| 2 | As User D, open Notifications | User D got "<User A> added you to <C1>"; the link opens C1 |
| 3 | As User A, click "Whole Team (N)" on the Users card | Dropdown: Everyone, User A's "(You)" row, then the people; User D is listed |
| 4 | Click the row of User D, type "hi" and send | The message with @User D is sent; no LLM response; User D becomes a participant |
| 5 | Type "@" in the message input | All teammates except User A, and Everyone, are listed and can be filtered |
| 6 | Send "@Everyone update" | Sent; User B and User D (every member with access) get a mention notification |
| 7 | As User D, click the mention notification | C1 opens at the message, no "not found" error |

---

## Expected Final State

Whole team access works for mentions and notifications like explicit access.

---

## Notes

- Depends on #7680, #7718; server part #7523.
