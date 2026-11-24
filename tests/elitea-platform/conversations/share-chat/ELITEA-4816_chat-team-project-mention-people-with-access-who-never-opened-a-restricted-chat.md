---
id: ELITEA-4816
title: "Chat – Team Project – Mention People with Access Who Never Opened a Restricted Chat"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, share-chat]
requirements: [EliteaAI/elitea_issues#7523]
---

# ELITEA-4816: Chat – Team Project – Mention People with Access Who Never Opened a Restricted Chat

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that in a chat shared with selected people, the owner can mention a selected person who has never opened the chat: the person becomes a participant once and is notified, and mentions of existing participants still work.

---

## Preconditions

- User is logged in to the Elitea platform.
- Team project; User A owns chat C1 shared (Share > Team) with User B and User C only.
- User B has already sent a message in C1 (is a participant); User C has never opened C1.
- User E is a project member without access to C1.
- Separate sessions for User A, User B, User C and User E.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, open C1 and click "3 users" on the Users card | Dropdown: Everyone, User A "(You)", then User B and User C; User E is not listed |
| 2 | Type "@" in the message input | Only User B, User C and Everyone are listed; User E is not |
| 3 | Click the row of User C in the Users dropdown, type "please check" and send | Message with @User C is sent without errors; no LLM response; User C becomes a participant of C1 |
| 4 | As User C, open Notifications and click the mention notification | One mention notification from User A; C1 opens at the message, no "not found" error |
| 5 | As User A, mention User C again and send; then mention User B and send | Both messages are sent; User C appears only once among participants; User B gets a mention notification |
| 6 | Send "@Everyone update" | User B and User C get a mention notification; User E gets nothing |

---

## Expected Final State

People with access are mentioned and notified whether or not they had opened the chat, without duplicates; people without access are not offered.
