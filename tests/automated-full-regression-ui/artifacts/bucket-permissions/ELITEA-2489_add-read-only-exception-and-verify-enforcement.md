---
id: ELITEA-2489
title: "Add Read-only Exception and Verify Enforcement"
priority: high
type: functional
module: artifacts
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:artifacts, nfr:security]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---

# ELITEA-2489: Add Read-only Exception and Verify Enforcement

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Add a user with "Read-only" permission, then login as that user and verify they can view and download files but cannot upload, delete, or modify content.

---

## Preconditions

- User A (Admin) is logged in to the Elitea platform (Team project)
- User B exists in the Team project with default permissions
- A test bucket "permissionstest" exists with at least 1 file

---

## Test Data

| Field | Value |
|-------|-------|
| Project | Team project (e.g., "Bugs & Features") |
| Project ID | 406 |
| Bucket name | permissionstest |
| User A | Admin user |
| User B | Test user for permission verification |
| Permission to set | Read-only |
| Test file | Any existing file in the bucket |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login as User A (Admin) | Login successful |
| 2 | Navigate to Artifacts and select bucket "permissionstest" | Bucket content displayed |
| 3 | Open Manage Permissions modal (context menu → Manage access) | Modal opens |
| 4 | Click "+" to add exception | Add exception modal opens |
| 5 | Select User B from Users dropdown | User B selected |
| 6 | Select "Read-only" permission | Permission selected |
| 7 | Click Save | User B added with "Read-only" |
| 8 | Verify User B appears in Exceptions with "Read-only" | User B listed correctly |
| 9 | Close modal and logout as User A | Logout successful |
| 10 | Login as User B | Login successful |
| 11 | Navigate to Artifacts | Artifacts page loads |
| 12 | Verify bucket "permissionstest" IS visible in sidebar | Bucket is visible |
| 13 | Click on the bucket | Bucket content (files) displayed |
| 14 | Verify files are listed in the file table | Files visible |
| 15 | Click preview on a file (if supported type) | Preview opens successfully |
| 16 | Click download on a file | File downloads successfully |
| 17 | Click Upload button | Red popup: "You have read-only permission for this bucket" |
| 18 | Right-click on a file to open context menu | Context menu opens |
| 19 | Verify Delete option behavior | Delete blocked with error message |
| 20 | Logout as User B | Logout successful |
| 21 | Login as User A | Login successful |
| 22 | Open Manage Permissions for the bucket | Modal opens |
| 23 | Edit User B's permission to "Read & Write" to clean up | User B removed from Exceptions |

---

## Expected Final State

User B with "Read-only" permission can see bucket, preview and download files, but cannot upload or delete. After cleanup, User B is restored to default.

---

## Pass/Fail Criteria

**Pass:**
- User B can see the bucket
- User B can preview and download files
- Upload is blocked with error message
- Delete is blocked with error message
- Cleanup restores User B to default

**Fail:**
- User B cannot see the bucket (too restrictive)
- Preview or download fails
- Upload succeeds (permission bypass)
- Delete succeeds (permission bypass)
