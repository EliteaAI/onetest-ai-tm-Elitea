---
id: ELITEA-2191
title: "Chat – Team Project – Non-Owner Cannot Regenerate LLM Response in Public Conversation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2191: Chat – Team Project – Non-Owner Cannot Regenerate LLM Response in Public Conversation

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that a non-owner cannot regenerate an LLM response in a public conversation.

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
| 2 | Hover over the last LLM response | Regenerate button NOT visible |
| 3 | Verify regenerate icon NOT present in response action icons | No regenerate icon |
| 4 | Verify only speaker and copy icons are available for non-owner | Only speaker and copy present |

---

## Expected Final State

Non-owner has no Regenerate button on LLM responses.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Regenerate not accessible to non-owner.

**Fail:**
- Any step produces an error or unexpected result.
- Non-owner can regenerate responses.
