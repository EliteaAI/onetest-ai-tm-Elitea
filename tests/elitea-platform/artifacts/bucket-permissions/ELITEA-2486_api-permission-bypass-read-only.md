---
id: ELITEA-2486
title: "API Permission Enforcement - Read-only User"
priority: critical
type: security
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:backend, r-2.0.5, nfr:security]
requirements: [EliteaAI/elitea_issues#5832]
---
# ELITEA-2486: API Permission Enforcement - Read-only User

**Module:** Artifacts · **Priority:** Critical · **Type:** Security

**Objective:** Verify that write operations are blocked at the API level for users with "Read-only" permission. GET should succeed, POST and DELETE should return 403 Forbidden.

**Coverage:**
- AC10 from Story #5832: Permissions cannot be bypassed

## Preconditions

- Two users: User A (Admin), User B (Team project member)
- A bucket exists with User B set to "Read-only" exception
- Access to Swagger UI

## Test Data

- Team project: "Bugs & Features" (project_id: 406)
- Bucket: `permissionstest`
- Filename: `manage_permissions_big_screen.png`
- User A: Admin with full access
- User B: Has "Read-only" exception for the bucket
- Swagger URLs:
  - GET: `https://dev.elitea.ai/shared/swagger/?all=true#/artifacts/get_api_v2_artifacts_artifact__mode___project_id___bucket___filename_`
  - POST: `https://dev.elitea.ai/shared/swagger/?all=true#/artifacts/post_api_v2_artifacts_artifacts__mode___project_id___bucket_`
  - DELETE: `https://dev.elitea.ai/shared/swagger/?all=true#/artifacts/delete_api_v2_artifacts_artifact__mode___project_id___bucket_`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Login as User A (Admin) | Login successful |
| 2 | Open Manage Permissions for bucket "permissionstest" | Modal opens |
| 3 | Add User B with "Read-only" permission | User B added to exceptions |
| 4 | Logout and login as User B | Login successful |
| 5 | Verify User B can see bucket in UI and download files | Bucket visible, download works |
| 6 | Open Swagger UI in the same browser (as User B) | Swagger loads with User B's session |
| 7 | Navigate to GET endpoint | Endpoint page opens |
| 8 | Fill parameters: mode=`default`, project_id=`406`, bucket=`permissionstest`, filename=`manage_permissions_big_screen.png` | Parameters filled |
| 9 | Execute GET request | Response: 200 OK with file content (Read works) |
| 10 | Navigate to POST endpoint (upload) | Endpoint page opens |
| 11 | Fill parameters: mode=`default`, project_id=`406`, bucket=`permissionstest`, select any file | Parameters filled |
| 12 | Execute POST request | Response: 403 Forbidden with error "You have read-only permission for this bucket" |
| 13 | Navigate to DELETE endpoint | Endpoint page opens |
| 14 | Fill parameters: mode=`default`, project_id=`406`, bucket=`permissionstest` | Parameters filled |
| 15 | Execute DELETE request | Response: 403 Forbidden with error "You have read-only permission for this bucket" |

## Expected Final State

GET succeeds (Read-only allows reading). POST and DELETE return 403 Forbidden.

## Pass/Fail Criteria

**Pass:**
- GET returns 200 OK with file content
- POST returns 403 Forbidden
- DELETE returns 403 Forbidden
- Read operations work, write operations are blocked

**Fail (SECURITY BUG):**
- POST succeeds (file uploaded)
- DELETE succeeds (file deleted)
- Any write operation bypasses Read-only restriction
