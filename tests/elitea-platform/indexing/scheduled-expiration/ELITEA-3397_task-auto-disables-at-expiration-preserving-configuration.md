---
id: ELITEA-3397
title: "Scheduled indexing task auto-disables at expiration and preserves its configuration"
priority: critical
type: functional
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with permission to create scheduled indexing tasks
- A scheduled indexing task exists whose expiration date can be reached (via backend time adjustment or waiting)

## Test Data

| Field | Value |
|-------|-------|
| Task Name | Expiration Auto-Disable Test |
| Source | Test Datasource |
| Schedule | Daily |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Advance/set the test task to its expiration date | Expiration date reached |
| 2 | Check task status | Status automatically changes to inactive/disabled without manual action |
| 3 | Wait past the next would-be scheduled run | No indexing run is triggered after expiration |
| 4 | Open the expired task's configuration (source, schedule, filters, credentials) | All configuration fields remain intact and unmodified |
| 5 | Check the task list | Task remains visible/accessible, not deleted or hidden |

## Expected Final State

Task is disabled at expiration, executes no further runs, and retains full configuration.

## Pass/Fail Criteria

**Pass:**
- Task auto-disables at expiration without manual action
- No indexing runs occur after expiration
- Configuration remains intact and the task stays visible in the task list

**Fail:**
- Task keeps running past its expiration date
- Task disappears from the task list
- Task loses configuration after expiring
