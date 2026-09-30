---
id: ELITEA-3527
title: "list_folders — List Mail Folders With Paging/Sorting"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3527: list_folders — List Mail Folders With Paging/Sorting

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `list_folders` returns the mailbox's folder tree and that the `sort_by` argument only accepts its literal enum values (`path`, `unread`, `total`), rejecting anything else.

## Preconditions

- Test mailbox has multiple folders (Inbox, Drafts, Sent Items, at least one custom folder)
- Toolkit with `list_folders` enabled

## Test Data

| Variant | sort_by | Expected |
|---|---|---|
| A | `path` | Accepted; folders sorted by path |
| B | `unread` | Accepted; folders sorted by unread count |
| C | `total` | Accepted; folders sorted by total item count |
| D | `name` | Rejected — not a valid enum value |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `list_folders` with Variant A | Full folder list returned, sorted by path |
| 2 | Invoke `list_folders` with Variant B | Folder list returned, sorted by unread count |
| 3 | Invoke `list_folders` with Variant C | Folder list returned, sorted by total item count |
| 4 | Invoke `list_folders` with Variant D (`sort_by="name"`) | Call rejected with a validation error naming the allowed enum values |

## Expected Final State

Folders list correctly for each valid sort mode; invalid `sort_by` values are rejected before any Graph call.

## Pass/Fail Criteria

**Pass:**
- All three valid `sort_by` values produce correctly ordered results
- Invalid `sort_by` is rejected with a clear validation error

**Fail:**
- Any valid sort mode returns incorrectly ordered results
- Invalid `sort_by` is silently accepted or defaults without error
