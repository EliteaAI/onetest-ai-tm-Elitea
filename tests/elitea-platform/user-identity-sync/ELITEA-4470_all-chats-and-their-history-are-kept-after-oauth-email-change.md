---
id: ELITEA-4470
title: "All chats and their history are kept after the user's email changes in the IdP"
priority: critical
type: functional
module: user-identity-sync
status: ready
execution_type: manual
tags: [feat:auth, feat:chat, int:oauth, issue:6184, email-change, p0]
requirements: ["EliteaAI/elitea_issues#6184"]
---

# ELITEA-4470: All chats and their history are kept after the user's email changes in the IdP

**Module:** user-identity-sync · **Priority:** Critical (P0) · **Type:** Functional

**Objective:** Verify that after the user's email changes in Keycloak, the user sees all their conversations with full history and can keep chatting in them.

---

## Preconditions

- Environment with the #6184 fix deployed (auth_oidc#3, auth_init#4, auth_core#22).
- A Keycloak realm admin who can edit users.
- A Keycloak user **U** who has logged in to Elitea at least once **after** the deploy, is a member of a team project **TP1**, and has an agent **A1** in the private project. Note U's user ID.
- **Setup (before the change):** create 3 conversations: **CH1** with the default model, **CH2** with A1 as a participant (both in the private project), and **CH3** in TP1. Send 3 or more messages in each. Note the number of messages in each.
- **Email change:** log U out. In Keycloak, change U's **Email** (and **Username**, if editable) to a new value and save.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to Elitea as U with the new credentials. Open Chat in the private project. | The user ID is the same. CH1 and CH2 are listed. |
| 2 | Open CH1. | All messages from the setup are shown, in order. U's messages are shown as U's. |
| 3 | Open CH2. | All messages are shown, including the agent replies. |
| 4 | Switch to TP1 and open CH3. | CH3 is listed with all its messages. |
| 5 | Send a new message in CH1 and in CH2. | Each message gets a reply. |
| 6 | Refresh the page and reopen CH1. | The old and new messages are still there. |

---

## Expected Final State

All three conversations belong to U and contain the setup messages plus the new ones.

---

## Pass/Fail Criteria

**Pass:**
- All conversations and their full history are shown, and new messages get replies.

**Fail:**
- Any conversation or message is missing, or U's earlier messages are shown as another user's.
- Sending a message fails with an access error.
