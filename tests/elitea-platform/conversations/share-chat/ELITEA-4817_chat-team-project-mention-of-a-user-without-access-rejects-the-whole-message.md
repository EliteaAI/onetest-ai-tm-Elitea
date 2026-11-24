---
id: ELITEA-4817
title: "Chat – Team Project – Mention of a User Without Access Rejects the Whole Message"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [feat:chat, share-chat]
requirements: [EliteaAI/elitea_issues#7523]
---

# ELITEA-4817: Chat – Team Project – Mention of a User Without Access Rejects the Whole Message

**Module:** conversations · **Priority:** high · **Type:** functional

**Objective:** Verify that a message mentioning someone who cannot open the chat is rejected as a whole with a clear error: nothing is saved, nobody is added as a participant, nobody is notified, and the chat keeps working.

---

## Preconditions

- User is logged in to the Elitea platform.
- Team project; User A owns chat C1 shared with User B and User C; neither has opened C1 yet.
- User A has C1 open in two browser tabs (Tab 1, Tab 2). Separate sessions for User B and User C.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Tab 1, click "3 users" on the Users card and keep the chat as is | User B and User C are listed in the dropdown |
| 2 | In Tab 2, open Share > Team, remove User B, Save | Toast "Access updated"; the Users card shows "2 users" |
| 3 | In Tab 1 (no reload), mention User B and User C in one message ("@User B @User C review") and send | The message is rejected with "<User B> can't be mentioned: they don't have access to this chat."; no endless spinner; the message does not appear in the chat |
| 4 | Reload Tab 1 and check the messages and the Users dropdown | The rejected message is not in the history; User B is not listed; User C is not added as a participant |
| 5 | As User B and as User C, open Notifications | Neither has a mention notification from the rejected message; User B cannot open C1 |
| 6 | As User A, mention User C alone and send | The message is sent; User C becomes a participant and gets a mention notification |

---

## Expected Final State

A mention of someone without access never sends a partly-mentioned message; the error names the person and the chat stays usable.
