---
id: ELITEA-2619
title: "Chat – New Message Sent Normally Immediately After Stop"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2619: Chat – New Message Sent Normally Immediately After Stop

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that immediately after stopping a generation, the user can send a new prompt (the restored one, or a different one) and get a normal response, with no leftover state from the stopped run.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| First message | "generate a long research summary" |
| Second message | "hello" |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Send the first message and click Stop during the thinking phase | Execution stops; input restored with first message text |
| 2 | Clear the input and type the second message ("hello") | Send button becomes active |
| 3 | Click Send | Second message is sent as a new user message |
| 4 | Verify a new response begins generating normally (thinking steps and/or streaming text as applicable) | New generation starts without errors |
| 5 | Wait for the response to complete | Full response is generated and displayed |
| 6 | Verify no error messages, duplicate messages, or references to the stopped first message appear | Chat continues cleanly |

---

## Expected Final State

A new message sent right after a stop is processed and answered normally, with no residual state from the previously stopped run.

---

## Pass/Fail Criteria

**Pass:**
- New message sends and receives a complete response without errors.
- No duplicate or stray messages related to the stopped run appear.

**Fail:**
- New message fails to send or generation does not start.
- Error messages appear, or duplicate/garbled messages are shown.
