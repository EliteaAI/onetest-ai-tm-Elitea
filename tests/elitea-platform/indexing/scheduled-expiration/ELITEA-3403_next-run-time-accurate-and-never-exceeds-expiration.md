---
id: ELITEA-3403
title: "Next run time for scheduled indexing tasks is accurate and never extends past expiration"
priority: high
type: functional
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with permission to view scheduled indexing tasks
- An active scheduled task exists with a defined frequency and expiration date

## Test Data

| Field | Value |
|-------|-------|
| Task Name | Next Run Boundary Test |
| Schedule | Daily |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the scheduled tasks list/management view | List loads |
| 2 | Check each active task's next run date/time next to its expiration date | Next run time displayed, calculated correctly from frequency and last run/creation date |
| 3 | Configure a test task so its next scheduled run would fall on/after its expiration date | Setup complete |
| 4 | Reach the expiration date | Task auto-disables; no next run is shown, executed, or pending beyond expiration |
| 5 | Check the last valid run before expiration | Executes normally and does not itself trigger premature expiration |

## Expected Final State

Next run time is accurate at all times and never exceeds the task's expiration boundary.

## Pass/Fail Criteria

**Pass:**
- Next run time is always displayed accurately and is never later than the task's expiration date
- The last valid run before expiration executes normally

**Fail:**
- A next run is shown, scheduled, or executed past the expiration date
- Next run time displayed does not match the actual calculated value
