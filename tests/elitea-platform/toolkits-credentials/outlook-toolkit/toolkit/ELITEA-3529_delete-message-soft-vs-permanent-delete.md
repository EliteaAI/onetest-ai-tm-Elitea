---
id: ELITEA-3529
title: "delete_message — Soft vs. Permanent Delete"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3529: delete_message — Soft vs. Permanent Delete

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `delete_message` moves a message to Deleted Items by default (`permanent=False`), and permanently removes it when `permanent=True` is explicitly set.

## Preconditions

- Two disposable test messages in the Inbox with known `message_id`s
- Toolkit with `delete_message` enabled

## Test Data

- Message A `message_id`: soft-delete target, `permanent` omitted (defaults to `False`)
- Message B `message_id`: permanent-delete target, `permanent=True`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `delete_message` on Message A without specifying `permanent` | Call succeeds |
| 2 | Check Deleted Items folder | Message A is present in Deleted Items |
| 3 | Invoke `delete_message` on Message B with `permanent=True` | Call succeeds |
| 4 | Check Deleted Items and search the whole mailbox for Message B | Message B is not in Deleted Items and not recoverable via mailbox search |

## Expected Final State

Message A is recoverable in Deleted Items; Message B is permanently removed.

## Pass/Fail Criteria

**Pass:**
- Default delete lands the message in Deleted Items
- `permanent=True` fully removes the message from the mailbox

**Fail:**
- Default delete permanently removes the message (bypassing Deleted Items)
- `permanent=True` leaves the message recoverable
