---
id: ELITEA-3756
title: "API: No Access Permission Enforcement (GET, POST, DELETE)"
priority: critical
type: security
module: artifacts
status: ready
execution_type: automated
tags: [automated:API:regression, feat:artifacts, nfr:security]
automation_test_id:
  - tests.ui.artifacts.test_bucket_permissions_api.TestBucketPermissionsAPI.test_no_access_permission_blocks_all_api_operations
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1577
requirements: [EliteaAI/elitea_issues#5832]
---

# ELITEA-3756: API: No Access Permission Enforcement (GET, POST, DELETE)

**Module:** artifacts · **Priority:** critical · **Type:** security

**Objective:** Verify that all API operations (GET, POST, DELETE) return 403 Forbidden for users with "No access" permission to a bucket. This test uses direct API calls to verify backend permission enforcement.

---

## Preconditions

- User A (Admin) is logged in to the Elitea platform (Team project)
- User B exists in the Team project
- A test bucket "permissionstest" exists with at least 1 file
- User B has "No access" exception set for the bucket

---

## Test Data

| Field | Value |
|-------|-------|
| Project | Team project "Bugs & Features" |
| Project ID | 406 |
| Bucket name | permissionstest |
| Test filename | manage_permissions_big_screen.png |
| User A | Admin user |
| User B | Test user with "No access" permission |
| API Base URL | https://dev.elitea.ai |
| GET/DELETE endpoint | /api/v2/artifacts/artifact/default/{project_id}/{bucket}/{filename} |
| POST endpoint | /api/v2/artifacts/artifacts/default/{project_id}/{bucket} |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | **[UI Setup]** Login as User A (Admin) | Login successful |
| 2 | **[UI Setup]** Navigate to Artifacts → bucket "permissionstest" | Bucket opens |
| 3 | **[UI Setup]** Open Manage Permissions modal | Modal opens |
| 4 | **[UI Setup]** Add User B with "No access" permission | User B added to Exceptions |
| 5 | **[UI Setup]** Logout as User A | Logout successful |
| 6 | **[UI Setup]** Login as User B | Login successful |
| 7 | **[UI Verify]** Navigate to Artifacts | Artifacts page loads |
| 8 | **[UI Verify]** Verify bucket "permissionstest" is NOT visible in sidebar | Bucket not listed (UI enforcement works) |
| 9 | **[API Test]** Execute GET request to `/api/v2/artifacts/artifact/default/406/permissionstest/manage_permissions_big_screen.png` using User B's session | Response: 403 Forbidden |
| 10 | **[API Test]** Verify GET response body contains error message | Error: "You do not have access to this bucket" |
| 11 | **[API Test]** Execute POST request to `/api/v2/artifacts/artifacts/default/406/permissionstest` with any file using User B's session | Response: 403 Forbidden |
| 12 | **[API Test]** Execute DELETE request to `/api/v2/artifacts/artifact/default/406/permissionstest` using User B's session | Response: 403 Forbidden |
| 13 | **[Cleanup]** Logout as User B | Logout successful |
| 14 | **[Cleanup]** Login as User A | Login successful |
| 15 | **[Cleanup]** Open Manage Permissions and edit User B to "Read & Write" | User B removed from Exceptions (restored to default) |

---

## API Request Details

### GET Request
```
GET /api/v2/artifacts/artifact/default/406/permissionstest/manage_permissions_big_screen.png
Headers: Cookie: centry_auth_session={User_B_session}
```

### POST Request
```
POST /api/v2/artifacts/artifacts/default/406/permissionstest
Headers: Cookie: centry_auth_session={User_B_session}
Content-Type: multipart/form-data
Body: file=@test_file.txt
```

### DELETE Request
```
DELETE /api/v2/artifacts/artifact/default/406/permissionstest
Headers: Cookie: centry_auth_session={User_B_session}
```

---

## Expected Final State

All API operations (GET, POST, DELETE) return 403 Forbidden for User B with "No access" permission. No bucket data is accessible or modifiable via direct API calls.

---

## Pass/Fail Criteria

**Pass:**
- GET returns 403 Forbidden (not 200 OK)
- POST returns 403 Forbidden (not 200/201)
- DELETE returns 403 Forbidden (not 200/204)
- Response bodies contain appropriate error messages
- Cleanup restores User B to default permissions

**Fail (SECURITY BUG):**
- GET returns 200 OK with file content
- POST returns success (file uploaded)
- DELETE returns success (file deleted)
- Any API operation bypasses "No access" restriction
