---
id: ELITEA-2483
title: "Read Permission Enforcement (UI)"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, eng:backend, r-2.0.5, nfr:security]
requirements: [EliteaAI/elitea_issues#5832]
---
# ELITEA-2483: Read Permission Enforcement (UI)

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that users with "Read" permission can view and download but cannot modify bucket content via UI.

**Coverage:**
- AC7 from Story #5832: Read access is enforced

## Preconditions

- Two users: User A (Admin), User B (Team project member)
- User is logged in to {{base_url}} (Team project)
- A bucket exists with files and User B set to "Read" exception

## Test Data

- Team project: "Bugs & Features"
- Bucket: "permissionstest" with at least 1 file and 1 folder
- User A: Admin
- User B: Has "Read-only" exception for the bucket

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Login as User A and set User B to "Read-only" for bucket | User B has Read-only exception |
| 2 | Logout and login as User B | Login successful |
| 3 | Navigate to Artifacts | Bucket "permissionstest" is visible in sidebar |
| 4 | Click on the bucket | Bucket content (files/folders) is displayed |
| 5 | Click on a folder | Folder expands showing contents |
| 6 | Click preview for a supported file (e.g., image, text) | File preview opens successfully |
| 7 | Click download for a file | File downloads successfully |
| 8 | Click Upload button and try to add file | Red popup message "You have read-only permission for this bucket" appears |
| 9 | Try to create a new folder (if option exists) | Red popup message appears |
| 10 | Try to rename a file via context menu | Red popup message appears |
| 11 | Try to move a file via context menu | Red popup message appears |
| 12 | Try to delete a file via context menu | Red popup message appears |

## Expected Final State

User B can view and download content but cannot upload, create, edit, rename, move, or delete anything.

## Pass/Fail Criteria

**Pass:**
- Bucket is visible and accessible
- Files can be listed, previewed, and downloaded
- Upload is blocked
- Create/Edit/Rename/Move/Delete actions are blocked

**Fail:**
- Bucket is not visible (too restrictive)
- Any write operation succeeds (insufficient restriction)
- Preview or download fails (too restrictive)
