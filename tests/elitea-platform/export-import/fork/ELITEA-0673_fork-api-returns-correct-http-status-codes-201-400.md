---
id: ELITEA-0673
title: "Fork API Returns Correct HTTP Status Codes (201 / 400)"
priority: high
type: functional
module: fork
status: ready
execution_type: manual
tags: [feat:import-forking, story:3728, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3728]
---
# ELITEA-0673: Fork API Returns Correct HTTP Status Codes (201 / 400)

**Module:** Fork · **Priority:** High · **Type:** Functional

**Objective:** Verify the `POST /api/v2/elitea_core/fork/prompt_lib/{project_id}` endpoint returns the correct HTTP status code based on outcome.

**Coverage:**
- HTTP 201 on full success
- HTTP 207 on partial success
- HTTP 400 on full failure
- Response body structure (`result`, `errors` keys)

## Preconditions

- Access to browser DevTools Network tab or API client (e.g. Postman)
- Logged in as Editor in Source and Target projects

## Test Data

- Endpoint: POST /api/v2/elitea_core/fork/prompt_lib/{target_project_id}
- Valid fork payload: properly structured applications array with one agent
- Invalid payload: empty JSON {}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open browser DevTools → Network tab; fork one valid agent to Target Project | Response received |
| 2 | Check the HTTP status code of the fork request | Status is 201 |
| 3 | Check the response body | result.agents contains the created entity; errors.agents is empty |
| 4 | Submit a fork with an invalid/empty payload using DevTools or API client | Response received |
| 5 | Check the HTTP status code | Status is 400 |
| 6 | Check the response body | errors key contains a descriptive error message |

## Expected Final State

errors key contains a descriptive error message

## Pass/Fail Criteria

**Pass:**
- 201 returned on clean success with result populated
- 400 returned on full failure with errors populated
- 207 returned on partial outcomes

**Fail:**
- All scenarios return 200 regardless of outcome
- Response body does not contain result and errors keys
- Status codes are inconsistent with actual outcome
