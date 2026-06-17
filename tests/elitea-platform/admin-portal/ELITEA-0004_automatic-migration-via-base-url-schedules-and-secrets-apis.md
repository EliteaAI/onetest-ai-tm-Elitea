---
id: ELITEA-0004
title: "Automatic Migration via Base URL - Schedules and Secrets APIs"
priority: high
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [base-url-inheritance, automatic-migration, schedules-api, secrets-api, issue:3879]
requirements: [3879]
---
# ELITEA-0004: Automatic Migration via Base URL - Schedules and Secrets APIs

**Module:** Admin Portal · **Priority:** High · **Type:** Functional

**Objective:** Verify that schedulesApi.js and secretsApi.js automatically migrated to v2 endpoints through the RTK Query baseUrl change without requiring code modifications

## Preconditions

Admin user access
Schedules management section available
Secrets management section available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to schedules management section | Schedules interface loads |
| 2 | Perform schedule operations (view, create, update) | All schedule operations use /api/v2/ endpoints |
| 3 | Navigate to secrets management section | Secrets interface loads |
| 4 | Perform secrets operations (view, create, update) | All secrets operations use /api/v2/ endpoints |
| 5 | Confirm automatic base URL inheritance | No v1 endpoint usage in either API |

## Expected Final State

No v1 endpoint usage in either API

## Pass/Fail Criteria

PASS: Schedules and secrets operations use v2 endpoints automatically via base URL inheritance
FAIL: Operations use v1 endpoints or automatic migration fails
