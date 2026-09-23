---
id: ELITEA-3404
title: "Expired scheduled indexing tasks list is available and supports quick rescheduling"
priority: high
type: functional
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with permission to view and reschedule scheduled indexing tasks
- At least one expired task exists alongside active tasks

## Test Data

| Field | Value |
|-------|-------|
| Expired Task | Test task past its expiration date |
| Active Task | Test task not yet expired |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the scheduled tasks area and locate the expired tasks list/filter | Expired list/filter is available |
| 2 | Check status indicators on expired entries | Clearly distinguished from active tasks (status label/visual indicator) |
| 3 | Check each expired entry for a reschedule action | Direct action/link to reschedule is present |
| 4 | Reschedule a task directly from this list | Task moves to (or is correctly reflected in) the active tasks view |

## Expected Final State

Expired tasks are easy to find and reschedule from a dedicated view.

## Pass/Fail Criteria

**Pass:**
- Expired tasks list/filter exists and clearly labels expired tasks
- Rescheduling from this list succeeds and updates the task's status

**Fail:**
- Expired tasks are not separately listed or distinguishable from active tasks
- Reschedule action is missing or fails from the expired task list
