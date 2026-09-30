---
id: ELITEA-3533
title: "get_thread_messages — Full Conversation Retrieval With New-Reply Detection"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3533: get_thread_messages — Full Conversation Retrieval With New-Reply Detection

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `get_thread_messages` returns every message in a conversation in order, and that `new_replies_count` correctly excludes replies sent by the mailbox owner themselves.

## Preconditions

- A thread from ELITEA-3524/ELITEA-3525 containing the original message and a reply
- A further external reply added to the same thread (from the secondary mailbox)
- Toolkit with `get_thread_messages` enabled

## Test Data

- `conversation_id` (or `message_id`) of the test thread

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Have the secondary/recipient mailbox reply into the thread | Thread now has: original message, owner's reply, external reply |
| 2 | Invoke `get_thread_messages` with the thread identifier | All three messages are returned, in chronological order |
| 3 | Inspect `new_replies_count` | Count reflects only the external reply, excluding the owner's own reply from ELITEA-3525 |

## Expected Final State

The full thread is returned in order, and `new_replies_count` accurately excludes the owner's own messages.

## Pass/Fail Criteria

**Pass:**
- All thread messages are returned in correct order
- `new_replies_count` excludes the owner's own replies

**Fail:**
- Thread retrieval misses a message or returns them out of order
- `new_replies_count` incorrectly includes the owner's own replies
