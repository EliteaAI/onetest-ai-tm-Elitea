---
id: ELITEA-1050
title: "API Health and Connectivity"
priority: critical
type: functional
module: smoke-suite
status: ready
execution_type: automated
automation_test_id:
  - test_api_health.py:TestAPIHealth.test_api_root_reachable
test_api_health.py:TestAPIHealth.test_api_returns_json
test_api_health.py:TestAuthenticatedAPI.test_list_agents
tags: []
requirements: []
---
# ELITEA-1050: API Health and Connectivity

**Module:** Smoke Suite · **Priority:** Critical · **Type:** Functional

**Objective:** Verify basic API connectivity and health checks for Elitea backend services.

**Coverage:**
- API root endpoint (`/api/v1`) is reachable
- API returns valid JSON responses
- List agents endpoint (`/api/v2/applications`) works

## Preconditions

- Network access to {{base_url}}
- A valid API token is available (from .env.test or system admin)
- A REST API testing tool is available (e.g., Postman, curl, or browser dev tools)

## Test Data

- API base URL: {{base_url}}
- Health check URL: {{base_url}}
- Project ID: 23

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a browser or API tool and send a GET request to {{base_url}} (the API health endpoint). | The server responds with an HTTP status code less than 500 (e.g., 200 OK, or 401/403 are acceptable). |
| 2 | Check the response Content-Type header from the previous request. | If the status was 200, the Content-Type includes 'json' or 'text'. |
| 3 | Send an authenticated GET request to the list agents endpoint: {{base_url}} with query parameter agents_type=classic. Include the API token in the Authorization header. | The response returns HTTP 200 with valid JSON data containing agent information. |

## Expected Final State

The response returns HTTP 200 with valid JSON data containing agent information.

## Pass/Fail Criteria

**Pass:**
- API root responds with status < 500
- Response Content-Type is valid (json or text)
- Authenticated list agents returns 200 with valid data structure

**Fail:**
- API returns 5xx error on root endpoint
- Content-Type header missing or invalid
- List agents returns non-200 status
- Response is not valid JSON (list or dict)
