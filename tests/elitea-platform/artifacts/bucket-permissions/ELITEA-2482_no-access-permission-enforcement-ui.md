---
id: ELITEA-2482
title: "No Access Permission Enforcement (UI)"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, eng:backend, r-2.0.5, nfr:security]
requirements: [EliteaAI/elitea_issues#5832]
---
# ELITEA-2482: No Access Permission Enforcement (UI)

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that users with "No access" permission cannot see or interact with the bucket via UI.

**Coverage:**
- AC6 from Story #5832: No access revokes bucket access

## Preconditions

- Two users: User A (Admin), User B (Team project member)
- User is logged in to {{base_url}} (Team project)
- A bucket exists with User B set to "No access" exception

## Test Data

- Team project: "Bugs & Features"
- Bucket: "permissionstest" (or any test bucket)
- User A: Admin with full access
- User B: Has "No access" exception for the bucket

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Login as User A (Admin) | Login successful |
| 2 | Navigate to Artifacts | Artifacts page opens |
| 3 | Open Manage Permissions for bucket "permissionstest" | Modal opens |
| 4 | Add User B with "No access" permission | User B added to exceptions |
| 5 | Logout and login as User B | Login successful |
| 6 | Navigate to Artifacts in the same Team project | Artifacts page opens |
| 7 | Look for bucket "permissionstest" in sidebar | Bucket is NOT visible in the bucket list |
| 8 | Try to navigate directly via URL to the bucket | Access denied or bucket not found error |

## Expected Final State

User B cannot see or access the bucket in any way via UI.

## Pass/Fail Criteria

**Pass:**
- Bucket is not visible in sidebar for User B
- Direct URL navigation fails for User B
- No files or folders from the bucket are accessible

**Fail:**
- Bucket appears in sidebar
- User B can navigate to bucket via URL
- User B can see or download any files
