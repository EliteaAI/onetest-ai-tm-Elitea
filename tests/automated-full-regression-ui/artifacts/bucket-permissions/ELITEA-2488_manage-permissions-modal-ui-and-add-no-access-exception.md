---
id: ELITEA-2488
title: "Manage Permissions Modal UI, and Enforcement of No Access and Read-only Exceptions"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts, nfr:security]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---

# ELITEA-2488: Manage Permissions Modal UI, and Enforcement of No Access and Read-only Exceptions

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify the Manage Permissions modal UI elements, then verify that a user granted "No access" cannot see or access the bucket, and that a user granted "Read-only" can view/download files but cannot upload, delete, or modify content.

---

## Preconditions

- User A (Admin) is logged in to the Elitea platform (Team project)
- User B exists in the Team project
- A test bucket "permissionstest" exists with at least 1 file
- User B has default permissions (not in Exceptions list)

---

## Test Data

| Field | Value |
|-------|-------|
| Project | Team project (e.g., "Bugs & Features") |
| Project ID | 406 |
| Bucket name | permissionstest |
| User A | Admin user |
| User B | Test user for permission verification |
| Test file | Any existing file in the bucket |

---

## Steps

### Part 1: Manage Permissions Modal UI

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Login as User A (Admin) | Login successful, dashboard displayed |
| 2 | Navigate to Artifacts section | Artifacts page loads |
| 3 | Verify bucket "permissionstest" is visible in sidebar | Bucket is listed |
| 4 | Click on context menu (3 dots) next to bucket name in sidebar | Context menu opens |
| 5 | Verify "Manage permissions" option is present in context menu | "Manage permissions" option visible |
| 6 | Click "Manage Permissions" | "Manage Permissions" modal opens |
| 7 | Verify modal header shows "Manage Permissions" with X close button | Header and close button present |
| 8 | Verify "Default Permissions" section shows "All users have read/write permissions by default." | Default permissions info displayed |
| 9 | Verify "Exceptions" section header with count | "Exceptions – N" displayed |
| 10 | Click "+" button to add exception | "Add exception" modal opens |
| 11 | Verify "Add exception" modal has Users dropdown and Permission dropdown | Both dropdowns present |
| 12 | Verify Permission dropdown has options: "No access", "Read-only" | Both options available |

### Part 2: "No Access" Exception Is Enforced

| # | Action | Expected Result |
|---|--------|-----------------|
| 13 | Search for User B in Users dropdown and select User B | User B added to selection |
| 14 | Select "No access" permission and click Save | Modal closes, User B added to Exceptions |
| 15 | Verify User B appears in Exceptions table with "No access" permission | User B listed with "No access" |
| 16 | Close Manage Permissions modal and logout as User A | Logout successful |
| 17 | Login as User B | Login successful |
| 18 | Navigate to Artifacts section | Artifacts page loads |
| 19 | Verify bucket "permissionstest" is NOT visible in sidebar | Bucket is NOT listed for User B |
| 20 | Logout as User B and login as User A | Login successful |
| 21 | Navigate to Artifacts and open Manage Permissions for the bucket, edit User B's permission to "Read & Write" to clean up | User B removed from Exceptions (restored to default) |

### Part 3: "Read-only" Exception Is Enforced

| # | Action | Expected Result |
|---|--------|-----------------|
| 22 | Open Manage Permissions modal, click "+" to add exception | Add exception modal opens |
| 23 | Select User B from Users dropdown, select "Read-only" permission, click Save | User B added with "Read-only" |
| 24 | Verify User B appears in Exceptions with "Read-only" | User B listed correctly |
| 25 | Close modal, logout as User A, login as User B | Login successful |
| 26 | Navigate to Artifacts | Artifacts page loads |
| 27 | Verify bucket "permissionstest" IS visible in sidebar | Bucket is visible |
| 28 | Click on the bucket; verify files are listed in the file table | Files visible |
| 29 | Click preview on a file (if supported type) | Preview opens successfully |
| 30 | Click download on a file | File downloads successfully |
| 31 | Click Upload button | Red popup: "You have read-only permission for this bucket" |
| 32 | Right-click on a file to open context menu; verify Delete option behavior | Delete blocked with error message |
| 33 | Logout as User B, login as User A | Login successful |
| 34 | Open Manage Permissions for the bucket, edit User B's permission to "Read & Write" to clean up | User B removed from Exceptions |

---

## Expected Final State

The Manage Permissions modal exposes all required UI elements. A user with "No access" cannot see the bucket at all. A user with "Read-only" can see the bucket, preview and download files, but cannot upload or delete. After cleanup, User B is restored to default permissions in both cases.

---

## Pass/Fail Criteria

**Pass:**
- All modal UI elements are present and functional.
- User B with "No access" cannot see the bucket when logged in.
- User B with "Read-only" can see the bucket, preview and download files; upload and delete are blocked with error messages.
- Cleanup restores User B to default permissions in both cases.

**Fail:**
- Modal UI elements missing or incorrect.
- User B can see the bucket with "No access" permission.
- User B cannot see the bucket with "Read-only" permission (too restrictive), or upload/delete succeeds (permission bypass).
- Cleanup fails.

---

## Notes

**Source functional tests:** ELITEA-2488, ELITEA-2489

**Regression rationale:** Both tests share an identical setup pattern (Admin adds an exception → logout → login as User B → verify sidebar visibility and allowed/blocked actions) and differ only in the permission level under test; consolidating into one test with shared modal-UI verification plus two enforcement parts avoids duplicated login/logout churn while preserving both checkpoints, mirroring the automated API-side pairing in ELITEA-3756/3757.

**Selected checkpoints:**
- Manage Permissions modal UI elements (ELITEA-2488)
- "No access" exception hides the bucket entirely (ELITEA-2488)
- "Read-only" exception allows view/download, blocks upload/delete (ELITEA-2489)
- Cleanup restores default permissions in both cases (ELITEA-2488, ELITEA-2489)
