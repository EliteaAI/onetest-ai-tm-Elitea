---
id: ELITEA-3714
title: "Verify user receives notification when indexing is stopped"
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
- User has a toolkit with a large data source (indexing takes several minutes)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start indexing for a large data source | Indexing begins, status shows "in_progress" |
| 2 | Navigate away to a different section | User is on different page |
| 3 | Return to Indexes and click "Stop" button | Indexing stops |
| 4 | Check notification bell/panel | Notification appears indicating indexing was stopped |
| 5 | Verify notification content | Notification shows index name and stopped status |

## Expected Final State

User receives a notification confirming indexing was stopped.

## Pass/Fail Criteria

**Pass:**
- Notification is received when indexing is stopped
- Notification clearly states the index was stopped (not failed)

**Fail:**
- No notification received after stopping indexing
- Notification incorrectly shows "failed" instead of "stopped"
