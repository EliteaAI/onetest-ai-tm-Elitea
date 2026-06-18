---
id: ELITEA-0008
title: "Mixed v1/v2 Environment Configuration Validation"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [environment-config, p0-critical, v1-v2-mixed, api-routing, issue:3879]
requirements: [3879]
---
# ELITEA-0008: Mixed v1/v2 Environment Configuration Validation

**Module:** Admin Portal · **Priority:** Critical · **Type:** Functional

**Objective:** Validate that the mixed v1/v2 environment configuration is correctly set up with V2_BASE and VITE_SERVER_URL environment variables properly configured and that the system handles both API versions simultaneously

## Preconditions

Admin access to environment configuration
Both v1 and v2 API services running
Admin panel access available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify V2_BASE environment variable configuration | V2_BASE points to /api/v2 |
| 2 | Verify VITE_SERVER_URL environment variable configuration | VITE_SERVER_URL points to /api/v1 |
| 3 | Test API calls that should use v2 endpoints | Calls correctly use V2_BASE configuration |
| 4 | Test API calls that should remain on v1 endpoints | Calls correctly use VITE_SERVER_URL configuration |
| 5 | Verify no cross-contamination between API versions | Each API call uses appropriate base URL |

## Expected Final State

Each API call uses appropriate base URL

## Pass/Fail Criteria

PASS: Both environment variables configured correctly and mixed API usage functions without conflicts
FAIL: Environment variable configuration errors or conflicts between v1/v2 API calls
