---
id: ELITEA-0009
title: "Broken Endpoints Resolution - Missing VITE_SERVER_URL Import Fix"
priority: critical
type: functional
module: admin-portal
status: draft
execution_type: manual
tags: [url-construction, projects-api, p0-critical, issue:4112, issue:3879, bug-fix]
requirements: [3879, 4112]
---
# ELITEA-0009: Broken Endpoints Resolution - Missing VITE_SERVER_URL Import Fix

**Module:** Admin Portal · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the missing VITE_SERVER_URL import in projectsApi.js is resolved, fixing the broken projectSuspend and projectUserActivity endpoints that were returning undefined URLs

## Preconditions

Admin user logged into ELITEA platform
Project management access available
Test projects available for operations

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to project management section | Project list loads successfully |
| 2 | Attempt to suspend a test project | Suspension operation completes without URL errors |
| 3 | Check network requests for projectSuspend endpoint | Valid URL with proper base path construction |
| 4 | Navigate to project user activity section | User activity data loads |
| 5 | Verify projectUserActivity endpoint URL construction | Valid URL without undefined components |

## Expected Final State

Valid URL without undefined components

## Pass/Fail Criteria

PASS: Both endpoints return valid responses with proper URL construction
FAIL: Either endpoint shows undefined URL or fails to execute due to URL construction error
