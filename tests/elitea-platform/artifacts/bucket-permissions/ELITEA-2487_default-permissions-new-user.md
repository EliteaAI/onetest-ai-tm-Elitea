---
id: ELITEA-2487
title: "Default Permissions for New Team Project Users"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:backend, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5832]
---
# ELITEA-2487: Default Permissions for New Team Project Users

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that new Team project members have default access (Read/Write) unless explicitly restricted.

**Coverage:**
- Migration requirements from Story #5832: Default behavior after migration
- "All users have read/write permissions by default" concept from #5912

## Preconditions

- Admin access to a Team project
- A new user account (or ability to add user to project)
- Existing buckets in the project

## Test Data

- Team project: "Bugs & Features"
- New User: A user not currently in the project
- Existing bucket: Any bucket without explicit exceptions for the new user

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Login as Admin | Login successful |
| 2 | Navigate to Settings → Users | Users list displayed |
| 3 | Add a new user to the Team project | User added successfully |
| 4 | Navigate to Artifacts and open Manage Permissions for a bucket | Modal opens |
| 5 | Verify new user is NOT in Exceptions table | User not listed (has default access) |
| 6 | Logout and login as the new user | Login successful |
| 7 | Navigate to Artifacts in the same Team project | Artifacts page opens |
| 8 | Verify all buckets are visible | All project buckets are shown in sidebar |
| 9 | Select a bucket and upload a file | Upload succeeds (Read/Write access works) |
| 10 | Delete the uploaded file | Delete succeeds |

## Expected Final State

New users have Read/Write access to all buckets by default (no explicit exception required).

## Pass/Fail Criteria

**Pass:**
- New user has access to all buckets without being in Exceptions table
- New user can perform all operations (Read/Write)
- "All users have read/write permissions by default" is accurate

**Fail:**
- New user cannot see buckets
- New user is automatically added to Exceptions
- Default access is restricted (No access or Read only)
