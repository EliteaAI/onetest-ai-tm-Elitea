---
id: ELITEA-3399
title: "Expiration notifications are sent at 7-day and 24-hour thresholds with task details and reschedule link"
priority: high
type: functional
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with access to the notification channel
- A scheduled indexing task exists with a known expiration date reachable in the test window

## Test Data

| Threshold |
|-----------|
| 7 days before expiration |
| 24 hours before expiration |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Advance/configure the task so expiration is 7 days away | Notification triggers at this threshold |
| 2 | Inspect the 7-day notification | Contains task name, source, current schedule, and a functional reschedule link |
| 3 | Advance/configure the task so expiration is 24 hours away | Second, distinct notification triggers |
| 4 | Inspect the 24-hour notification | Contains task details and a functional reschedule link; content differs from the 7-day notification (not a duplicate) |
| 5 | Click each reschedule link | Navigates to the correct task's reschedule/edit view |

## Expected Final State

Both threshold notifications are delivered once each, with correct content and working links.

## Pass/Fail Criteria

**Pass:**
- Both notifications fire exactly once at their respective thresholds
- Each notification contains correct task details and a working reschedule link

**Fail:**
- A notification is missing, duplicated, or delivered at the wrong time
- A reschedule link is broken or points to the wrong task
