---
id: ELITEA-2488
title: "Manage Permissions Modal UI and Add No Access Exception"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts, nfr:security]
requirements: [EliteaAI/elitea_issues#5832, EliteaAI/elitea_issues#5912]
---

# ELITEA-2488: Manage Permissions Modal UI and Add No Access Exception

**Module:** artifacts · **Priority:** high · **Type:** functional

**Objective:** Verify the Manage Permissions modal UI elements, add a user with "No access" permission, then login as that user and verify they cannot see or access the bucket.

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
| Permission to set | No access |

---

## Steps

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
| 12 | Search for User B in Users dropdown | User B appears in dropdown |
| 13 | Select User B | User B added to selection |
| 14 | Verify Permission dropdown has options: "No access", "Read-only" | Both options available |
| 15 | Select "No access" permission | "No access" selected |
| 16 | Click Save | Modal closes, User B added to Exceptions |
| 17 | Verify User B appears in Exceptions table with "No access" permission | User B listed with "No access" |
| 18 | Close Manage Permissions modal | Modal closes |
| 19 | Logout as User A | Logout successful |
| 20 | Login as User B | Login successful |
| 21 | Navigate to Artifacts section | Artifacts page loads |
| 22 | Verify bucket "permissionstest" is NOT visible in sidebar | Bucket is NOT listed for User B |
| 23 | Logout as User B | Logout successful |
| 24 | Login as User A | Login successful |
| 25 | Navigate to Artifacts and open Manage Permissions for the bucket | Modal opens |
| 26 | Edit User B's permission to "Read & Write" to clean up | User B removed from Exceptions (restored to default) |

---

## Expected Final State

User B with "No access" permission cannot see the bucket in the Artifacts sidebar. After cleanup, User B is restored to default permissions.

---

## Pass/Fail Criteria

**Pass:**
- All modal UI elements are present and functional
- User B is successfully added with "No access" permission
- User B cannot see the bucket when logged in
- Cleanup restores User B to default permissions

**Fail:**
- Modal UI elements missing or incorrect
- Cannot add User B to Exceptions
- User B can still see the bucket with "No access" permission
- Cleanup fails
