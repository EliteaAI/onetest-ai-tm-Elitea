---
id: ELITEA-2479
title: "Edit Single Permission Exception"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---
# ELITEA-2479: Edit Single Permission Exception

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that a user can edit a single permission exception. Setting "Read & Write" removes the user from Exceptions (returns to default access).

**Coverage:**
- AC5 from Story #5832: User can update bucket permissions
- AC7 from Story #5912: User can edit a single user's permission exception

## Preconditions

- User is logged in to {{base_url}} (Team project)
- User has permission to manage bucket access
- A bucket exists with at least one user in Exceptions list with "Read-only" permission

## Test Data

- Team project with Admin role
- Bucket with existing exception (e.g., User A with "Read-only" permission)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Manage Permissions modal for a bucket | Modal opens with Exceptions table |
| 2 | Locate a user row with "Read-only" permission | User row is visible |
| 3 | Click Edit (pencil) icon in the row's Actions column | Edit modal opens for that user |
| 4 | Verify current permission is shown | "Read-only" is selected in Permission dropdown |
| 5 | Change permission to "No access" | New permission selected |
| 6 | Click Save | Modal closes |
| 7 | Verify updated permission in table | User now shows "No access" permission |
| 8 | Click Edit for the same user again | Edit modal opens |
| 9 | Verify current permission is "No access" | "No access" is selected |
| 10 | Change permission to "Read & Write" | "Read & Write" selected |
| 11 | Click Save | Modal closes |
| 12 | Verify user is removed from Exceptions table | User no longer appears in Exceptions table (returned to default access) |

## Expected Final State

User permission is updated; setting "Read & Write" removes the user from the Exceptions table (as Read & Write is the default permission for all users).

## Pass/Fail Criteria

**Pass:**
- Edit modal shows current permission
- Permission can be changed between "No access", "Read-only", and "Read & Write"
- Save updates the table immediately
- "Read & Write" removes user from Exceptions table (returns to default)

**Fail:**
- Edit modal doesn't pre-select current permission
- Save doesn't update the table
- "Read & Write" doesn't remove user from Exceptions table
