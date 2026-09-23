---
id: ELITEA-3400
title: "Rescheduling an active scheduled indexing task resets its expiration date"
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
- An active scheduled indexing task exists nearing its expiration date

## Test Data

| Field | Value |
|-------|-------|
| Task Name | Reschedule Reset Test |
| Original Frequency | Weekly |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the current expiration date of the active task | Expiration date recorded |
| 2 | Reschedule the task (re-save with same or updated frequency) via the reschedule link or task settings | Reschedule action succeeds |
| 3 | Check the task's expiration date after rescheduling | New expiration date calculated from the current date and applicable frequency-tier rule |
| 4 | Wait past the original expiration date/notification thresholds | No stale 7-day/24-hour notifications are sent for the superseded expiration date |

## Expected Final State

Task expiration timer is reset to a new date on reschedule, and stale notifications are suppressed.

## Pass/Fail Criteria

**Pass:**
- Expiration date resets correctly upon reschedule
- No stale notifications fire for the previous expiration date

**Fail:**
- Expiration date remains unchanged after rescheduling
- Stale notifications still arrive for the superseded expiration date
