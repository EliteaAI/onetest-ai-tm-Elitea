---
id: ELITEA-3713
title: "Verify user receives notification when indexing completes"
priority: critical
type: functional
module: indexes
status: draft
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has a toolkit with indexing capability configured
- Notifications are enabled for the user

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start indexing for a toolkit | Indexing begins, status shows "in_progress" |
| 2 | Navigate away to a different section | User is on different page |
| 3 | Wait for indexing to complete | Indexing finishes |
| 4 | Check notification bell/panel | Notification appears indicating indexing completed |
| 5 | Verify notification content | Notification shows index name and "completed" status |

## Expected Final State

User receives a notification confirming successful indexing completion.

## Pass/Fail Criteria

**Pass:**
- Notification is received when indexing completes
- Notification clearly states index name and success status

**Fail:**
- No notification received after indexing completes
- Notification is delayed by more than 1 minute after completion
