---
id: ELITEA-3406
title: "Expiration notifications are suppressed for manually disabled or already-expired tasks"
priority: medium
type: functional
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with permission to manage scheduled indexing tasks and access notifications
- A manually disabled task and an already-expired task exist

## Test Data

| Field | Value |
|-------|-------|
| Disabled Task | Active task manually disabled before its expiration date |
| Expired Task | Task already past its expiration date |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Manually disable an active task well before its expiration date | Task disabled |
| 2 | Wait past the 7-day and 24-hour thresholds for this task | No expiration notifications are sent |
| 3 | Observe an already-expired task over time | No repeated/duplicate notifications are generated after it became inactive |

## Expected Final State

No expiration notifications are generated for tasks that are disabled or already expired.

## Pass/Fail Criteria

**Pass:**
- No 7-day or 24-hour notifications are sent for a manually disabled task
- No repeated notifications are generated for an already-expired task

**Fail:**
- A notification is sent for a manually disabled task
- Duplicate or repeated notifications occur for an already-expired task
