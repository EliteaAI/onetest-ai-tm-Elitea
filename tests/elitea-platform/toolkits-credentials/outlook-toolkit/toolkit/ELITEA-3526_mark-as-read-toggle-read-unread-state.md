---
id: ELITEA-3526
title: "mark_as_read — Toggle Read/Unread State"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3526: mark_as_read — Toggle Read/Unread State

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `mark_as_read` can both mark a message as read and, when supported, mark it back as unread, with the mailbox state reflecting the change.

## Preconditions

- A known unread message in the test mailbox (`message_id` known)
- Toolkit with `mark_as_read` enabled

## Test Data

- `message_id`: an unread test message
- `is_read = True`, then `is_read = False`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `mark_as_read` with `message_id` and `is_read=True` | Call succeeds |
| 2 | Use `get_message` or check the mailbox client | Message is now marked as read |
| 3 | Invoke `mark_as_read` with the same `message_id` and `is_read=False` | Call succeeds |
| 4 | Re-check the message state | Message is now marked as unread again |

## Expected Final State

The message's read/unread state accurately reflects the last `mark_as_read` call.

## Pass/Fail Criteria

**Pass:**
- Message state toggles correctly in both directions

**Fail:**
- State does not change after the call
- Call errors out for either direction
