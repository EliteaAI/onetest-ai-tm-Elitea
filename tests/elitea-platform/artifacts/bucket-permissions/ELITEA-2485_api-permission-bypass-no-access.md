---
id: ELITEA-2485
title: "API Permission Enforcement - No Access User"
priority: critical
type: security
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, bug-area:current-release-scope, eng:backend, r-2.0.5, nfr:security]
requirements: [EliteaAI/elitea_issues#5832]
---
# ELITEA-2485: API Permission Enforcement - No Access User

**Module:** Artifacts · **Priority:** Critical · **Type:** Security

**Objective:** Verify that bucket permissions are enforced at the API level for users with "No access" permission. All operations (GET, POST, DELETE) should return 403 Forbidden.

**Coverage:**
- AC10 from Story #5832: Permissions cannot be bypassed

## Preconditions

- Two users: User A (Admin), User B (Team project member)
- A bucket exists with User B set to "No access" exception
- Access to Swagger UI

## Test Data

- Team project: "Bugs & Features" (project_id: 406)
- Bucket: `permissionstest`
- Filename: `manage_permissions_big_screen.png`
- User A: Admin with full access
- User B: Has "No access" exception for the bucket
- Swagger URLs:
  - GET: `https://dev.elitea.ai/shared/swagger/?all=true#/artifacts/get_api_v2_artifacts_artifact__mode___project_id___bucket___filename_`
  - POST: `https://dev.elitea.ai/shared/swagger/?all=true#/artifacts/post_api_v2_artifacts_artifacts__mode___project_id___bucket_`
  - DELETE: `https://dev.elitea.ai/shared/swagger/?all=true#/artifacts/delete_api_v2_artifacts_artifact__mode___project_id___bucket_`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Login as User A (Admin) | Login successful |
| 2 | Open Manage Permissions for bucket "permissionstest" | Modal opens |
| 3 | Add User B with "No access" permission | User B added to exceptions |
| 4 | Verify User B cannot see bucket in UI | Bucket not visible in sidebar |
| 5 | Open Swagger UI in the same browser (as User B) | Swagger loads with User B's session |
| 6 | Navigate to GET endpoint | Endpoint page opens |
| 7 | Fill parameters: mode=`default`, project_id=`406`, bucket=`permissionstest`, filename=`manage_permissions_big_screen.png` | Parameters filled |
| 8 | Execute GET request | Response: 403 Forbidden with error "You have no access to this bucket" |
| 9 | Navigate to POST endpoint (upload) | Endpoint page opens |
| 10 | Fill parameters: mode=`default`, project_id=`406`, bucket=`permissionstest`, select any file | Parameters filled |
| 11 | Execute POST request | Response: 403 Forbidden |
| 12 | Navigate to DELETE endpoint | Endpoint page opens |
| 13 | Fill parameters: mode=`default`, project_id=`406`, bucket=`permissionstest` | Parameters filled |
| 14 | Execute DELETE request | Response: 403 Forbidden |

## Expected Final State

All API operations (GET, POST, DELETE) return 403 Forbidden for "No access" user.

## Pass/Fail Criteria

**Pass:**
- GET returns 403 Forbidden
- POST returns 403 Forbidden
- DELETE returns 403 Forbidden
- No bucket data is accessible via API

**Fail (SECURITY BUG):**
- GET returns 200 OK with file content
- POST succeeds (file uploaded)
- DELETE succeeds (file deleted)
- Any operation bypasses "No access" restriction

## Known Issue

Currently there is a bug where GET returns 403 with message "You have read-only permission for this bucket" even for "No access" users. The error message is incorrect but the request is blocked. See issue #5965.
