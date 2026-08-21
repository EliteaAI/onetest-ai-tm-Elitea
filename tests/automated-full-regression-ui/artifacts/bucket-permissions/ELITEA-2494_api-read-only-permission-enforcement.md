---
id: ELITEA-2494
title: "API: Read-only Permission Enforcement (GET allowed, POST/DELETE blocked)"
priority: critical
type: security
module: artifacts
status: ready
execution_type: automated
tags: [automated:API:regression, feat:artifacts, nfr:security]
automation_test_id:
  - tests.ui.artifacts.test_bucket_permissions_api.TestBucketPermissionsAPI.test_read_only_permission_allows_get_blocks_write_operations
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1577
requirements: [EliteaAI/elitea_issues#5832]
---

# ELITEA-2494: API: Read-only Permission Enforcement (GET allowed, POST/DELETE blocked)

**Module:** artifacts · **Priority:** critical · **Type:** security

**Objective:** Verify that for users with "Read-only" permission: GET operations succeed (200 OK), while POST and DELETE operations return 403 Forbidden. This test uses direct API calls to verify backend permission enforcement.

---

## Preconditions

- User A (Admin) is logged in to the Elitea platform (Team project)
- User B exists in the Team project
- A test bucket "permissionstest" exists with at least 1 file
- User B has "Read-only" exception set for the bucket

---

## Test Data

| Field | Value |
|-------|-------|
| Project | Team project "Bugs & Features" |
| Project ID | 406 |
| Bucket name | permissionstest |
| Test filename | manage_permissions_big_screen.png |
| User A | Admin user |
| User B | Test user with "Read-only" permission |
| API Base URL | https://dev.elitea.ai |
| GET endpoint | /api/v2/artifacts/artifact/default/{project_id}/{bucket}/{filename} |
| POST endpoint | /api/v2/artifacts/artifacts/default/{project_id}/{bucket} |
| DELETE endpoint | /api/v2/artifacts/artifact/default/{project_id}/{bucket} |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | **[UI Setup]** Login as User A (Admin) | Login successful |
| 2 | **[UI Setup]** Navigate to Artifacts → bucket "permissionstest" | Bucket opens |
| 3 | **[UI Setup]** Open Manage Permissions modal | Modal opens |
| 4 | **[UI Setup]** Add User B with "Read-only" permission | User B added to Exceptions |
| 5 | **[UI Setup]** Logout as User A | Logout successful |
| 6 | **[UI Setup]** Login as User B | Login successful |
| 7 | **[UI Verify]** Navigate to Artifacts | Artifacts page loads |
| 8 | **[UI Verify]** Verify bucket "permissionstest" IS visible in sidebar | Bucket is listed (Read access works) |
| 9 | **[API Test]** Execute GET request to `/api/v2/artifacts/artifact/default/406/permissionstest/manage_permissions_big_screen.png` using User B's session | Response: 200 OK with file content |
| 10 | **[API Test]** Verify GET response contains file data | File content returned successfully |
| 11 | **[API Test]** Execute POST request to `/api/v2/artifacts/artifacts/default/406/permissionstest` with any file using User B's session | Response: 403 Forbidden |
| 12 | **[API Test]** Verify POST response body contains error message | Error: "You have read-only permission for this bucket" |
| 13 | **[API Test]** Execute DELETE request to `/api/v2/artifacts/artifact/default/406/permissionstest` using User B's session | Response: 403 Forbidden |
| 14 | **[API Test]** Verify DELETE response body contains error message | Error: "You have read-only permission for this bucket" |
| 15 | **[Cleanup]** Logout as User B | Logout successful |
| 16 | **[Cleanup]** Login as User A | Login successful |
| 17 | **[Cleanup]** Open Manage Permissions and edit User B to "Read & Write" | User B removed from Exceptions (restored to default) |

---

## API Request Details

### GET Request (Should Succeed)
```
GET /api/v2/artifacts/artifact/default/406/permissionstest/manage_permissions_big_screen.png
Headers: Cookie: centry_auth_session={User_B_session}
Expected: 200 OK with file content
```

### POST Request (Should Fail)
```
POST /api/v2/artifacts/artifacts/default/406/permissionstest
Headers: Cookie: centry_auth_session={User_B_session}
Content-Type: multipart/form-data
Body: file=@test_file.txt
Expected: 403 Forbidden
```

### DELETE Request (Should Fail)
```
DELETE /api/v2/artifacts/artifact/default/406/permissionstest
Headers: Cookie: centry_auth_session={User_B_session}
Expected: 403 Forbidden
```

---

## Expected Final State

GET operations succeed for User B with "Read-only" permission (read access works). POST and DELETE operations return 403 Forbidden (write operations blocked).

---

## Pass/Fail Criteria

**Pass:**
- GET returns 200 OK with file content
- POST returns 403 Forbidden with error message "You have read-only permission for this bucket"
- DELETE returns 403 Forbidden with error message "You have read-only permission for this bucket"
- Cleanup restores User B to default permissions

**Fail (SECURITY BUG):**
- GET fails with 403 (too restrictive for Read-only user)
- POST returns success (file uploaded — permission bypass)
- DELETE returns success (file deleted — permission bypass)
- Any write operation bypasses Read-only restriction
