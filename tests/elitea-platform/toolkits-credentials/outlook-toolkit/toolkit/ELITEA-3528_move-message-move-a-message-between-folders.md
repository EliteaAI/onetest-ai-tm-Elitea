---
id: ELITEA-3528
title: "move_message — Move a Message Between Folders"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3528: move_message — Move a Message Between Folders

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `move_message` relocates a message to the target folder and that the message is no longer present in the source folder afterward.

## Preconditions

- A known test message in the Inbox (`message_id` known)
- A destination folder (e.g. "Archive" or a custom test folder) exists
- Toolkit with `move_message` enabled

## Test Data

- `message_id`: a test message in Inbox
- `destination_folder`: `Archive`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `move_message` with the test `message_id` and `destination_folder=Archive` | Call succeeds |
| 2 | Invoke `list_messages` on Inbox | The message no longer appears in Inbox |
| 3 | Invoke `list_messages` on Archive | The message now appears in Archive |

## Expected Final State

The message exists only in the destination folder; it is fully removed from the source folder.

## Pass/Fail Criteria

**Pass:**
- Message appears in destination and is absent from source after the move

**Fail:**
- Message appears in both folders, or in neither, after the call
- Call fails despite valid folder names
