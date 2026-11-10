---
id: ELITEA-4469
title: "Cross-user import correctly keeps the original author's display name on their own messages, even though the importer is the one added as participant"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, chat-import, cross-account, issue:6904, p1]
requirements: ["EliteaAI/elitea_issues#6904"]
---

# ELITEA-4469: Cross-user import correctly keeps the original author's display name on their own messages, even though the importer is the one added as participant

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that when User B imports a chat originally created and exported by User A, User B (the importer) is added as the chat's participant, User A is not added, but the message originally sent by User A still correctly displays "User A" as the sender. This is correct, expected behavior — not a bug.

---

## Preconditions

- Two user accounts: "User A" and "User B".

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As User A, create a chat. Send a first message, e.g. "Hi". | Chat created, authored by User A. |
| 2 | As User A, export this chat. | Export succeeds. |
| 3 | As User B, import the exported file into User B's own project. | User B (the importer) is added as the chat's participant. User A (the original author) is not added as a participant. The message originally sent by User A still clearly displays "User A" as the sender — not User B's name — even though User B is the one who imported and now owns the chat. |

## Expected Final State

Cross-user author attribution is correctly preserved in message display, independent of who actually owns/imported the chat.

## Pass/Fail Criteria

**Pass:**
- User B is the participant; User A's name still shows correctly on User A's own message. This is correct, expected behavior — not a bug.

**Fail:**
- User A's name being lost or replaced with User B's.
