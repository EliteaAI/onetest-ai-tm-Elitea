---
id: ELITEA-2183
title: "Chat – After Stopping Generation New Message Can Be Sent Normally"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2183: Chat – After Stopping Generation New Message Can Be Sent Normally

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that after stopping a generation during the thinking/sub-agent phase, a new message can be sent and the LLM responds normally, with no trace of the stopped exchange left in the chat history.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| First message | generate a poem |
| Second message | hello |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Type the first message and click Send; verify stop button appears once thinking/sub-agent steps begin | Stop button visible during thinking phase |
| 2 | Click stop button to cancel generation | Generation stops; input bar restored with the exact original first message text |
| 3 | Verify no user or assistant bubble remains in the chat for the stopped exchange | Chat looks as if the first message was never sent |
| 4 | Clear the input, type 'hello' in the message field | Send button appears |
| 5 | Click Send | New message sent; new LLM response begins |
| 6 | Verify no error messages shown | Chat continues normally |

---

## Expected Final State

New message can be sent after stopping previous generation; no trace of the stopped exchange remains in chat history.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Stopped exchange leaves no trace in chat history.
- New message sent and responded to after stopping.

**Fail:**
- Any step produces an error or unexpected result.
- Stopped exchange leaves a visible partial/empty message in the chat.
- Cannot send new message after stopping.
