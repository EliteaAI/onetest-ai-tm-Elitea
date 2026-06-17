---
id: ELITEA-0010
title: "Base URL Migration Validation - RTK Query v1 to v2 Transition"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [api-migration, p0-critical, admin-panel, issue:3879, rtk-query]
requirements: [3879]
---
# ELITEA-0010: Base URL Migration Validation - RTK Query v1 to v2 Transition

**Module:** Admin Portal · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the RTK Query baseUrl change from VITE_SERVER_URL (/api/v1) to V2_BASE (/api/v2) is correctly implemented in adminApi.js and that all admin panel endpoints now use the v2 API base URL

## Preconditions

Admin user logged into ELITEA platform
Admin panel access available
Both v1 and v2 API environments configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to admin panel | Admin panel loads successfully |
| 2 | Open browser developer tools Network tab | Network monitoring is active |
| 3 | Refresh admin panel and interact with various admin functions | Admin functions execute |
| 4 | Examine network requests for API calls | All admin API requests show /api/v2/ base URL |
| 5 | Verify no v1 endpoint calls are made | No /api/v1/ requests in admin operations |

## Expected Final State

No /api/v1/ requests in admin operations

## Pass/Fail Criteria

PASS: All admin API calls use v2 endpoints with 200/2xx responses
FAIL: Any admin API call uses v1 endpoint or returns v1-specific errors
