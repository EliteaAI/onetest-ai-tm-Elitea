---
id: ELITEA-0007
title: "User List Endpoint v1 Retention - Status Field Dependency Validation"
priority: high
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [mixed-api-versions, status-field, v1-retention, issue:3879, users-api]
requirements: [3879]
---
# ELITEA-0007: User List Endpoint v1 Retention - Status Field Dependency Validation

**Module:** Admin Portal · **Priority:** High · **Type:** Functional

**Objective:** Verify that the userList endpoint in usersApi.js correctly remains on v1 API due to the status field dependency, while other user endpoints migrate to v2 as intended

## Preconditions

Admin user access
User management section available
Multiple users in system for testing

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to user management section | User list loads successfully |
| 2 | Monitor network requests for userList API call | userList uses /api/v1/ endpoint |
| 3 | Verify user status field is present in response data | Status field visible in user list data |
| 4 | Test other user management operations (create, update, delete) | Other operations use /api/v2/ endpoints |
| 5 | Confirm no API version conflicts in mixed usage | All operations complete successfully |

## Expected Final State

All operations complete successfully

## Pass/Fail Criteria

PASS: userList uses v1 with status field, other user endpoints use v2, no API conflicts
FAIL: userList migrated to v2 incorrectly or status field missing from responses
