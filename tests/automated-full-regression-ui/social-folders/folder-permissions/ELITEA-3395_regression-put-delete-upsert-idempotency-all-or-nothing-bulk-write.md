---
id: ELITEA-3395
title: "[Regression] PUT/DELETE Folder Exceptions — Upsert, Idempotency, All-or-Nothing Bulk Write"
priority: high
type: integration
module: social-folders
status: draft
execution_type: manual
tags: [feat:social-folders, feat:roles-permissions, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6524]
---
# ELITEA-3395: [Regression] PUT/DELETE Folder Exceptions — Upsert, Idempotency, All-or-Nothing Bulk Write

**Module:** Social Folders · **Priority:** High · **Type:** Integration

**Objective:** Regression consolidation of the folder-access write path's core data-integrity guarantees: idempotent upsert, all-or-nothing bulk validation, and idempotent delete.

**Coverage:**
- Story #6524: Manage Folder-Level Permissions for Project Entities in Team Projects

## Preconditions
- Admin logged in; target folder has no pre-existing exceptions for the test users used

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | PUT `read_only` for User A, then PUT `no_access` for User A again | Second call overwrites the first — exactly one row for User A, now `no_access` |
| 2 | Repeat the exact same PUT body once more | Still exactly one row for User A (idempotent upsert, no duplicate) |
| 3 | PUT a batch containing User B (valid) and one entry with an invalid `access_level` | `400`; GET confirms User B was **not** partially written |
| 4 | DELETE User A's exception, then DELETE it again | Both calls return `200`; the second is a no-op with no error |

## Expected Final State
No leftover override rows for User A or User B at the end of the run.

## Pass/Fail Criteria
**Pass:**
- Upsert never duplicates, repeat writes are idempotent, an invalid entry fails the whole batch with zero partial writes, and DELETE is idempotent

**Fail:**
- Any duplicate row appears
- A partial write occurs after a rejected batch
- A repeat DELETE errors
