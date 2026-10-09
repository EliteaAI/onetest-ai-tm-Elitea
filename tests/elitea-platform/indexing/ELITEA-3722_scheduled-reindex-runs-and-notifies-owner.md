---
id: ELITEA-3722
title: "Verify scheduled reindex runs and notifies owner"
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
- User has permission to create scheduled reindex

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Schedule | Near-future time (e.g., 5 minutes from now) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure a scheduled reindex for an existing index | Schedule is saved |
| 2 | Wait for scheduled time | Reindex starts automatically |
| 3 | Wait for reindex to complete | Reindex completes |
| 4 | Check notifications | Schedule owner receives notification |
| 5 | Verify notification content | Notification indicates scheduled reindex completed |

## Expected Final State

Scheduled reindex executes at the configured time and the owner receives notification.

## Pass/Fail Criteria

**Pass:**
- Scheduled reindex runs at the configured time
- Owner receives notification upon completion

**Fail:**
- Scheduled reindex does not run
- No notification sent to the schedule owner
