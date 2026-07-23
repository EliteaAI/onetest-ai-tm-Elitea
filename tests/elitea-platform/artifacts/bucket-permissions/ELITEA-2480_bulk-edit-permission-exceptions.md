---
id: ELITEA-2480
title: "Bulk Edit Permission Exceptions"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---
# ELITEA-2480: Bulk Edit Permission Exceptions

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that users can bulk edit multiple permission exceptions at once. Setting "Read & Write" removes selected users from Exceptions (returns to default access).

**Coverage:**
- AC9 from Story #5832: Bulk actions are supported (edit)
- AC8 from Story #5912: User can bulk-edit multiple permission exceptions

## Preconditions

- User is logged in to {{base_url}} (Team project)
- User has permission to manage bucket access
- A bucket exists with at least 3 users in Exceptions list

## Test Data

- Team project with Admin role
- Bucket with 3+ exceptions (e.g., User A - Read-only, User B - Read-only, User C - No access)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Manage Permissions modal for a bucket | Modal opens with Exceptions table |
| 2 | Note current exception count (e.g., 3) | "Exceptions – 3" shown |
| 3 | Click checkbox in table header (Select All) | All user rows are selected (all checkboxes checked) |
| 4 | Click checkbox in table header again | All user rows are deselected (all checkboxes unchecked) |
| 5 | Click checkbox for User A row | User A is selected (checkbox checked) |
| 6 | Click checkbox for User B row | User B is selected (checkbox checked) |
| 7 | Verify bulk Edit icon is enabled above table | Bulk Edit (pencil) icon is clickable |
| 8 | Click bulk Edit icon | Bulk edit modal opens |
| 9 | Verify modal indicates multiple users selected | Shows count or list of selected users |
| 10 | Select "No access" permission | Permission selected |
| 11 | Click Save | Modal closes |
| 12 | Verify User A permission in table | Shows "No access" |
| 13 | Verify User B permission in table | Shows "No access" |
| 14 | Verify User C permission unchanged | Still shows original "No access" permission |
| 15 | Click checkbox in table header (Select All) | All users selected |
| 16 | Click bulk Edit icon | Bulk edit modal opens |
| 17 | Select "Read & Write" permission | Permission selected |
| 18 | Click Save | Modal closes |
| 19 | Verify all users are removed from table | Users no longer appear in Exceptions (returned to default) |
| 20 | Verify empty state is displayed | Empty state with "No exceptions added yet" appears |

## Expected Final State

All selected users have updated permission; setting "Read & Write" removes them from Exceptions table (returns to default access).

## Pass/Fail Criteria

**Pass:**
- Header checkbox selects/deselects all rows
- Multiple rows can be selected via individual checkboxes
- Bulk Edit applies same permission to all selected users
- Unselected users are not affected
- Table updates immediately after save
- "Read & Write" removes selected users from Exceptions table

**Fail:**
- Header checkbox doesn't work (select all / deselect all)
- Cannot select multiple rows
- Bulk edit affects unselected users
- Table doesn't reflect changes
- "Read & Write" doesn't remove users from Exceptions
