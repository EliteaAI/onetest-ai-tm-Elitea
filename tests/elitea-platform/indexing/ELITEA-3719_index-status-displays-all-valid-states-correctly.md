---
id: ELITEA-3719
title: "Verify index status displays all valid states correctly"
priority: high
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User can trigger various indexing scenarios

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Expected statuses | created, in_progress, completed, failed, stopped, partly_indexed |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new index without starting | Status shows "created" |
| 2 | Start indexing | Status shows "in_progress" |
| 3 | Let indexing complete successfully | Status shows "completed" |
| 4 | Trigger indexing with invalid source | Status shows "failed" |
| 5 | Stop indexing mid-process | Status shows "stopped" |
| 6 | Trigger partial indexing (some docs fail) | Status shows "partly_indexed" |

## Expected Final State

All six status values are displayed correctly in the UI based on the indexing outcome.

## Pass/Fail Criteria

**Pass:**
- All statuses (created, in_progress, completed, failed, stopped, partly_indexed) display correctly
- Status accurately reflects the actual indexing state

**Fail:**
- Any status displays incorrectly or is missing
- Status shows generic value instead of specific state
