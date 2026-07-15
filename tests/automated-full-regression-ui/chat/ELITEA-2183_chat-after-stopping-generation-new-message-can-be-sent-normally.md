---
id: ELITEA-2183
title: "Chat – After Stopping Generation New Message Can Be Sent Normally"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2183: Chat – After Stopping Generation New Message Can Be Sent Normally

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that after stopping a generation, a new message can be sent and the LLM responds normally.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Second message | hello |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Type a message and click Send; verify stop button appears | Stop button visible |
| 2 | Click stop button to cancel generation | Generation stops; input bar restored |
| 3 | Type 'hello' in the message field | Send button appears |
| 4 | Click Send | New message sent; new LLM response begins |
| 5 | Verify no error messages shown | Chat continues normally |

---

## Expected Final State

New message can be sent after stopping previous generation.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- New message sent and responded to after stopping.

**Fail:**
- Any step produces an error or unexpected result.
- Cannot send new message after stopping.
