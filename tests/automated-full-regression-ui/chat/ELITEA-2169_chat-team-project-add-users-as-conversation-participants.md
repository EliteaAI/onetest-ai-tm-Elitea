---
id: ELITEA-2169
title: "Chat – Team Project – Add Users as Conversation Participants"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2169: Chat – Team Project – Add Users as Conversation Participants

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that users can be added as conversation participants via the Invite Users modal.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Team project with an existing conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Users | user_1, user_2 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats in Team project and open any conversation | Conversation is open |
| 2 | Click + icon, select Invite Users | 'Add users' modal opens |
| 3 | Select user_1 from the dropdown; verify chip appears | user_1 chip visible |
| 4 | Select user_2 from the dropdown; verify chip appears | user_2 chip visible |
| 5 | Click Add | Modal closes; user_1 and user_2 in PARTICIPANTS USERS section |

---

## Expected Final State

Users added as conversation participants.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Users added correctly.

**Fail:**
- Any step produces an error or unexpected result.
- Users not added.
