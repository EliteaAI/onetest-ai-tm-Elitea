---
id: ELITEA-2484
title: "Read/Write Permission Enforcement (UI)"
priority: high
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:frontend, eng:backend, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5832]
---
# ELITEA-2484: Read/Write Permission Enforcement (UI)

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that users with "Read & Write" permission can perform all operations on bucket content via UI.

**Coverage:**
- AC8 from Story #5832: Read/Write access is enforced

## Preconditions

- Two users: User A (Admin), User B (Team project member)
- User is logged in to {{base_url}} (Team project)
- A bucket exists with files and User B set to "Read & Write" exception

## Test Data

- Team project: "Bugs & Features"
- Bucket: "permissionstest" with at least 1 file
- User A: Admin
- User B: Has "Read & Write" exception for the bucket
- Test file: Any small file for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Login as User A and set User B to "Read & Write" for bucket | User B has Read & Write exception |
| 2 | Logout and login as User B | Login successful |
| 3 | Navigate to Artifacts and select the bucket | Bucket content is displayed |
| 4 | Preview a file | Preview works |
| 5 | Download a file | Download works |
| 6 | Upload a new file | Upload succeeds, file appears in list |
| 7 | Create a new folder | Folder created successfully |
| 8 | Rename the uploaded file | File renamed successfully |
| 9 | Move the file to the created folder | File moved successfully |
| 10 | Delete the file | File deleted successfully |
| 11 | Delete the folder | Folder deleted successfully |

## Expected Final State

User B can perform all read and write operations on bucket content.

## Pass/Fail Criteria

**Pass:**
- All read operations work (view, preview, download)
- All write operations work (upload, create, edit, rename, move, delete)

**Fail:**
- Any operation fails
- User cannot access bucket at all
