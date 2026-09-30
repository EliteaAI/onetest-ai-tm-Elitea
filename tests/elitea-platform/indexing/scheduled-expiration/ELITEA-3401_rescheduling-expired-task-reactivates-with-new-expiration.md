---
id: ELITEA-3401
title: "Rescheduling an expired indexing task reactivates it and assigns a new expiration date"
priority: high
type: functional
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with permission to edit scheduled indexing tasks
- An expired/inactive scheduled indexing task exists

## Test Data

| Field | Value |
|-------|-------|
| Task Name | Expired Reactivation Test |
| Status | Expired/Inactive |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Locate the expired task in the expired task list | Task found, marked as expired/inactive |
| 2 | Initiate reschedule/reactivate action on the task | Action available and executes |
| 3 | Check task status after rescheduling | Status changes back to active |
| 4 | Check the new expiration date | Correctly calculated based on the task's (possibly updated) frequency |
| 5 | Wait for the next scheduled run | Indexing run resumes per schedule |

## Expected Final State

Expired task is reactivated, running again with a fresh expiration date.

## Pass/Fail Criteria

**Pass:**
- Task reactivates and status changes to active
- New expiration date is correctly calculated and indexing runs resume

**Fail:**
- Task fails to reactivate
- Task keeps the old or no expiration date after reactivation
- Indexing runs do not resume after reactivation
