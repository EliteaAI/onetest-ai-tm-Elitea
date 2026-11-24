---
id: ELITEA-2167
title: "Chat – Team Project – Create New Conversation and Add Users via Share Chat"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-2167: Chat – Team Project – Create New Conversation and Add Users via Share Chat

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify the complete flow of creating a conversation in a Team project and adding/cancelling/closing users via the Team tab of the Share Chat window.

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
| 1 | Navigate to Chats in Team project and click + Chat | New conversation opens; PARTICIPANTS panel visible |
| 2 | Click "+" in the message input | No 'Invite Users' item in the menu |
| 3 | Hover the Users card and click its Share icon (or "⋮" > Share) | Share Chat window opens on Team; "People with access – 1" |
| 4 | Focus the search, type 'sa' and select a user; type 'ad' and select a second user; click Add | Both users are listed after the owner; count = 3 |
| 5 | Click Save | Toast "Access updated"; the Users card shows "3 users" |
| 6 | Add a third user, click Cancel, then Leave | Window closes; third user not added (card still "3 users") |
| 7 | Add a fourth user, click × of the window, then Leave | Window closes; fourth user not added |
| 8 | Type 'hi all' and click Send | Message sent; LLM responds |
| 9 | Verify conversation appears in Today with multi-person icon | Conversation listed with users icon |

---

## Expected Final State

Conversation created with users added via Share Chat; Cancel and × dismiss without adding.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Users added via Add and Save; Cancel/× don't add users; the Users card count is correct.

**Fail:**
- Any step produces an error or unexpected result.
- Users not added or Cancel adds users.
