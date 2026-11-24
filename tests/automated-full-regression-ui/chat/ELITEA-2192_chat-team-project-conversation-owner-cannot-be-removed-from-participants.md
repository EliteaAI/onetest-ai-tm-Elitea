---
id: ELITEA-2192
title: "Chat – Team Project – Chat Owner Cannot Be Removed from Access"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: [EliteaAI/elitea_issues#7489]
---

# ELITEA-2192: Chat – Team Project – Chat Owner Cannot Be Removed from Access

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that the chat owner cannot be removed from the chat access: no delete in the users dropdown and no × for the owner in the Share Chat window.

---

## Preconditions

- User is logged in to the Elitea platform.
- The user owns a conversation shared with multiple people.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open the conversation | PARTICIPANTS panel with the Users card visible |
| 2 | Click the Users card count to open the users dropdown | Owner row first with the badge "Owner"; no delete on any row |
| 3 | Open Share > Team and hover the owner row | Owner listed first with "Owner"; no × |
| 4 | Click "Remove access for all", then Save | Only the owner remains; count = 1; the Users card shows "Only You" |
| 5 | Reopen the users dropdown and the Share window | Owner still listed |

---

## Expected Final State

Owner cannot be removed from the chat access.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No delete or × for the owner; owner kept after "Remove access for all".

**Fail:**
- Any step produces an error or unexpected result.
- Owner can be removed.
