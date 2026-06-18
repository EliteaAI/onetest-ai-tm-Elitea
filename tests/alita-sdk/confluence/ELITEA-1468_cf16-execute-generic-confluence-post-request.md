---
id: ELITEA-1468
title: "CF16 - Execute Generic Confluence (POST Request)"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [execute_generic_confluence, post-request, confluence, api]
requirements: []
---
# ELITEA-1468: CF16 - Execute Generic Confluence (POST Request)

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify execute_generic_confluence tool handles POST requests with data payload, adding a label to a page and returning an HTTP response string with status code (200 or 201).

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID env var is set
Valid Confluence REST API POST endpoint and existing page ID available for label operation

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
HTTP method: POST
API endpoint: '/rest/api/content/{CF_PAGE_ID}/label'
Payload: [{\"name\": \"test-label-cf16\", \"prefix\": \"global\"}]
CF_PAGE_ID: ID of existing page to add label to

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call execute_generic_confluence tool with method='POST', target endpoint for adding a label to a page (e.g., '/rest/api/content/{CF_PAGE_ID}/label'), and label data payload | Tool executes successfully with POST method and data payload |
| 2 | LLM validates: response contains HTTP status code 200 or 201, response text confirms label operation, POST method handled correctly | Validation confirms execute_generic_confluence handles POST requests with data payload correctly |

## Expected Final State

Validation confirms execute_generic_confluence handles POST requests with data payload correctly

## Pass/Fail Criteria

PASS: POST request executes, response returns status 200 or 201 with response text
FAIL: Tool crashes, wrong HTTP method used, non-2xx status without expected behavior
