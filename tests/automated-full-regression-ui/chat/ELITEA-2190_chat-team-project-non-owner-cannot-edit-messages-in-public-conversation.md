---
id: ELITEA-2190
title: "Chat – Team Project – Non-Owner Cannot Edit Messages in Public Conversation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2190: Chat – Team Project – Non-Owner Cannot Edit Messages in Public Conversation

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that a non-owner cannot edit messages in a public conversation.

---

## Preconditions

- User is logged in to the Elitea platform.
- Logged in as a non-owner user in a Team project with a public conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Open a public conversation owned by another user | Full history visible |
| 2 | Hover over any user message in the conversation | No pencil (edit) icon appears |
| 3 | Verify non-owner cannot trigger edit mode on any message | Edit mode not accessible |

---

## Expected Final State

Non-owner cannot edit messages.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No edit icon for non-owner.

**Fail:**
- Any step produces an error or unexpected result.
- Non-owner can edit messages.
