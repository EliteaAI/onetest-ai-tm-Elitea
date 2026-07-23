---
id: ELITEA-2481
title: "Remove Permission Exceptions via Edit to Read & Write"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---
# ELITEA-2481: Remove Permission Exceptions via Edit to Read & Write

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that permission exceptions can be removed by changing permission to "Read & Write" (default access). There is no separate Delete button — users are removed from Exceptions by restoring default access.

**Coverage:**
- AC6 from Story #5832: No access revokes bucket access; Read & Write is default
- AC9 from Story #5912: User can remove permission exceptions

## Preconditions

- User is logged in to {{base_url}} (Team project)
- User has permission to manage bucket access
- A bucket exists with at least 3 users in Exceptions list

## Test Data

- Team project with Admin role
- Bucket with 3+ exceptions (e.g., User A - No access, User B - Read-only, User C - No access)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Manage Permissions modal for a bucket | Modal opens with Exceptions table |
| 2 | Note current exception count (e.g., 3) | "Exceptions – 3" shown |
| 3 | Verify there is NO Delete (trash) icon in User A's row | No delete button exists; only Edit (pencil) icon |
| 4 | Click Edit (pencil) icon for User A | Edit modal opens |
| 5 | Change permission to "Read & Write" | Permission selected |
| 6 | Click Save | Modal closes |
| 7 | Verify User A is removed from table | User A no longer appears in Exceptions |
| 8 | Verify exception count decreased | "Exceptions – 2" shown |
| 9 | Select checkboxes for remaining users (User B, User C) | Both rows selected |
| 10 | Click bulk Edit icon | Bulk edit modal opens |
| 11 | Select "Read & Write" permission | Permission selected |
| 12 | Click Save | Modal closes |
| 13 | Verify both users are removed from table | User B and User C no longer appear |
| 14 | Verify empty state is displayed | Empty state with "No exceptions added yet" appears |

## Expected Final State

All users removed from Exceptions by setting "Read & Write" permission; empty state appears when all exceptions are removed.

## Pass/Fail Criteria

**Pass:**
- No Delete button exists in UI (only Edit)
- Setting "Read & Write" removes user from Exceptions table
- Exception count updates correctly
- Bulk edit to "Read & Write" removes all selected users
- Empty state appears when all exceptions are removed

**Fail:**
- Delete button exists (should not)
- "Read & Write" doesn't remove user from table
- Count doesn't update
- Bulk operation fails
