---
id: ELITEA-3713
title: "Indexing Control and Notifications"
priority: critical
type: functional
module: indexes
status: draft
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

# ELITEA-3713: Indexing Control and Notifications

**Module:** indexes · **Priority:** critical · **Type:** functional

**Objective:** Verify indexing completion and stop notifications are received, and Stop button correctly terminates indexing.

## Preconditions

- User is logged in to `{{base_url}}`
- User has toolkit with indexing capability configured
- Notifications are enabled

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **COMPLETION NOTIFICATION** | | |
| 1 | Start indexing for a toolkit | Indexing begins, status "in_progress" |
| 2 | Navigate away to different section | User on different page |
| 3 | Wait for indexing to complete | Indexing finishes |
| 4 | Check notification bell/panel | Notification appears: indexing completed |
| 5 | Verify notification content | Shows index name and "completed" status |
| **STOP NOTIFICATION & BUTTON** | | |
| 6 | Start new indexing operation | Indexing begins |
| 7 | While indexing in progress, click Stop button | Stop button clicked |
| 8 | Verify indexing stops | Status changes to "stopped" |
| 9 | Verify stopped status displayed | UI shows stopped state |
| 10 | Check notification panel | Notification appears: indexing stopped |
| 11 | Verify stop notification content | Shows index name and "stopped" status |

## Pass/Fail Criteria

**Pass:** Completion notification received; Stop button stops indexing; stopped notification received.
**Fail:** No notifications OR Stop button doesn't work OR status incorrect.

## Notes

**Source:** ELITEA-3713 (completion notif), ELITEA-3714 (stop notif), ELITEA-3715 (stop button)
**Rationale:** Consolidates indexing control & notifications: completion notif validates async updates; stop button + notification validates user control over long operations.
