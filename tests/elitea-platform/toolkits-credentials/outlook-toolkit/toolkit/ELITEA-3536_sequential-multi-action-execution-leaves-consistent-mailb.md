---
id: ELITEA-3536
title: "Sequential Multi-Action Execution Leaves Consistent Mailbox State"
priority: high
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3536: Sequential Multi-Action Execution Leaves Consistent Mailbox State

**Module:** Outlook Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify a chain of dependent Outlook actions run in sequence (send → search → mark read → move → delete) each act on the correct message and leave the mailbox in the expected final state.

## Preconditions

- Toolkit with all relevant tools enabled, linked to an authorized credential

## Test Data

- Subject: `Outlook Toolkit Test — sequential-chain {{timestamp}}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | `send_mail` a test message to the secondary mailbox | Message sent |
| 2 | `search_messages` in Sent Items for the exact subject to obtain its `message_id` | Correct message found |
| 3 | `mark_as_read` on that `message_id` with `is_read=True` | Message marked read |
| 4 | `move_message` on that `message_id` to an "Archive" folder | Message moved |
| 5 | `search_messages` scoped to Archive for the subject, then `delete_message` on the found `message_id` | Message found in Archive and deleted (soft delete) |
| 6 | Verify final mailbox state | Message is present only in Deleted Items; it is absent from Sent Items/Archive/Inbox |

## Expected Final State

The message ends up solely in Deleted Items, confirming every step in the chain operated on the correct message.

## Pass/Fail Criteria

**Pass:**
- Every step in the chain succeeds and operates on the correct message
- Final mailbox state matches expectations exactly

**Fail:**
- Any step operates on the wrong message (e.g. due to ID mix-up)
- Final state is inconsistent (message duplicated, lost, or left in an unexpected folder)
