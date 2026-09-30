---
id: ELITEA-3525
title: "reply_to_message — Reply Within an Existing Thread"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3525: reply_to_message — Reply Within an Existing Thread

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `reply_to_message` sends a reply that stays within the original message's conversation thread, and that the recipient receives it correctly threaded.

## Preconditions

- An existing message (from ELITEA-3524) with a known `message_id` to reply to
- Toolkit with `reply_to_message` enabled

## Test Data

- `message_id`: from the message sent in ELITEA-3524
- Reply body: `This is an automated reply.`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `reply_to_message` with the original `message_id` and reply body | Call succeeds |
| 2 | Check the original recipient's mailbox | Reply arrives threaded under the original conversation (same `conversationId`) |
| 3 | Use `get_thread_messages` on the conversation | Both the original message and the new reply appear in the thread |

## Expected Final State

The reply is delivered and correctly threaded with the original message.

## Pass/Fail Criteria

**Pass:**
- Reply is delivered with matching `conversationId`
- Thread retrieval shows both original and reply

**Fail:**
- Reply is sent as a new, unthreaded message
- Reply fails to send or is missing from the thread
