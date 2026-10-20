---
id: ELITEA-3715
title: "Verify Stop button stops indexing and shows stopped status"
priority: critical
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has a toolkit with large data source configured
- Indexing is currently in progress

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start indexing for a toolkit | Status changes to "in_progress" |
| 2 | While indexing is running, locate the "Stop" button | Stop button is visible and enabled |
| 3 | Click the "Stop" button | Confirmation dialog appears (if applicable) |
| 4 | Confirm stopping | Indexing process stops |
| 5 | Verify index status | Status shows "stopped" (not "failed" or "in_progress") |
| 6 | Verify partial progress is recorded | Indexed count shows documents processed before stopping |

## Expected Final State

Index status displays "stopped" with accurate count of documents indexed before stopping.

## Pass/Fail Criteria

**Pass:**
- Stop button is visible during indexing
- Clicking Stop changes status to "stopped"
- Partial progress count is preserved

**Fail:**
- Stop button is missing or disabled
- Status shows "failed" instead of "stopped"
- Indexed count resets to zero
