---
id: ELITEA-2622
title: "Chat – Stop Signal Correctly Bound to Task ID Under Fast Sequential Stop-Then-Resend"
priority: low
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, eng:backend, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2622: Chat – Stop Signal Correctly Bound to Task ID Under Fast Sequential Stop-Then-Resend

**Module:** chat-interface / streaming · **Priority:** Low (edge case) · **Type:** Functional

**Objective:** In a single conversation, verify that stopping one generation and then immediately starting a new one in quick succession does not cause the stop signal to leak forward and interrupt the new (second) generation.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| First message | "generate a detailed technical explanation of TCP handshakes" |
| Second message | "generate a short haiku about autumn" |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Send the first message and click Stop during the thinking phase | First generation stops; input restored with first message text |
| 2 | Immediately clear the input, type the second message, and click Send as fast as possible after the stop | Second message is sent, associated with a new task |
| 3 | Observe the second generation's thinking/streaming progress fully | Second generation proceeds and completes normally, uninterrupted |
| 4 | Verify the second response is not stopped prematurely or contaminated by the prior stop signal | Full, complete response for the second message is produced |

---

## Expected Final State

The stop signal from the first (cancelled) task does not affect the immediately-following second generation; each stop request is correctly scoped to its own task_id.

---

## Pass/Fail Criteria

**Pass:**
- The second generation runs to completion without being interrupted.
- No error or premature stop is observed on the second message.

**Fail:**
- The second generation is stopped/interrupted despite not being explicitly cancelled.
- Any cross-task interference is observed between the stopped first task and the new second task.
