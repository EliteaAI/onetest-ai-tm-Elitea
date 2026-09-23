---
id: ELITEA-3402
title: "Active scheduled indexing tasks display their expiration date in list and detail views"
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
- At least one active scheduled task with a calculated expiration date exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Task Name | Expiration Display Test |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the scheduled tasks list/management view | List loads with active tasks |
| 2 | Check each active task's row/card | Expiration date displayed in a clear, human-readable format |
| 3 | Open an individual task's detail view | Expiration date is also shown there |
| 4 | Compare displayed value to the stored expiration date | Values match |

## Expected Final State

Expiration dates are consistently visible across list and detail views.

## Pass/Fail Criteria

**Pass:**
- Expiration date is shown correctly in both the list and detail views
- Displayed value matches the stored expiration date

**Fail:**
- Expiration date is missing or malformed in either view
- Displayed value does not match the stored expiration date
