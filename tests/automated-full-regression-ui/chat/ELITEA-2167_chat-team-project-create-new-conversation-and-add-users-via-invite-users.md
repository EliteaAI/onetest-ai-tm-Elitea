---
id: ELITEA-2167
title: "Chat – Team Project – Create New Conversation and Add Users via Invite Users with Add Confirmation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2167: Chat – Team Project – Create New Conversation and Add Users via Invite Users with Add Confirmation

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the complete flow of creating a conversation in a Team project and adding/cancelling/closing users via the Invite Users modal.

---

## Preconditions

- User is logged in to the Elitea platform.
- User is in a Team project.

---

## Test Data

| Field | Value |
|-------|-------|
| Users to add | Hrach Sargsyan, Admin Bot | Search partial | sa, ad | Test message | hi all |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats in Team project and click + Chat | New conversation opens; PARTICIPANTS panel visible with empty USERS section |
| 2 | Click + icon and verify 'Invite Users' is in the menu | Invite Users option present |
| 3 | Click Invite Users | 'Add users' modal opens with search field and Cancel/Add buttons |
| 4 | Search 'sa' and select first user (e.g. Hrach Sargsyan) | User chip appears; modal stays open |
| 5 | Search 'ad' and select second user (e.g. Admin Bot) | Two user chips shown; modal stays open |
| 6 | Click Add button | Modal closes; both users in PARTICIPANTS USERS section |
| 7 | Click + icon, Invite Users, select a third user, click Cancel | Modal closes; third user not added |
| 8 | Click + icon, Invite Users, select a fourth user, click X (close) | Modal closes; fourth user not added |
| 9 | Type 'hi all' and click Send | Message sent; LLM responds; owner avatar added to PARTICIPANTS USERS |
| 10 | Verify conversation appears in Today with multi-person icon | Conversation listed with users icon |

---

## Expected Final State

Conversation created with users added; Cancel and X dismiss without adding; first message shows owner in PARTICIPANTS.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Users added via Add; Cancel/X don't add users; owner appears after first message.

**Fail:**
- Any step produces an error or unexpected result.
- Users not added or Cancel adds users.
