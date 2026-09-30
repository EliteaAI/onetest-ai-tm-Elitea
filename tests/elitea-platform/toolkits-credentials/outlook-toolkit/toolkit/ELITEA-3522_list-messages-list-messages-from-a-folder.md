---
id: ELITEA-3522
title: "list_messages — List Messages From a Folder"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3522: list_messages — List Messages From a Folder

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `list_messages` returns mailbox messages, respects the `folder` argument, and enforces the `limit` bounds (1–1000).

## Preconditions

- Toolkit with `list_messages` enabled, linked to an authorized credential
- Test mailbox contains messages in at least Inbox and one other folder (e.g. Drafts)

## Test Data

| Variant | folder | limit | Expected |
|---|---|---|---|
| A | (default) Inbox | 10 | Up to 10 Inbox messages returned |
| B | `Drafts` | 5 | Up to 5 Drafts messages returned |
| C | Inbox | 0 | Rejected — below minimum bound (1) |
| D | Inbox | 1001 | Rejected — above maximum bound (1000) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `list_messages` with Variant A | Returns up to 10 messages from Inbox with expected fields (subject, sender, received date) |
| 2 | Invoke `list_messages` with Variant B | Returns up to 5 messages from Drafts folder specifically |
| 3 | Invoke `list_messages` with Variant C (`limit=0`) | Call is rejected with a validation error referencing the limit bound |
| 4 | Invoke `list_messages` with Variant D (`limit=1001`) | Call is rejected with a validation error referencing the limit bound |

## Expected Final State

Messages are correctly listed and scoped per folder; out-of-bounds limits are rejected before any Graph call.

## Pass/Fail Criteria

**Pass:**
- Correct messages returned per folder for in-bounds limits
- Both out-of-bounds limit values are rejected with a clear validation error

**Fail:**
- Wrong folder's messages returned
- Out-of-bounds limit is silently accepted or clamped without error
