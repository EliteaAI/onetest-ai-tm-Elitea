---
id: ELITEA-1689
title: "XR01 - execute_graphql: Execute Custom GraphQL Query"
priority: medium
type: functional
module: xray
status: failed
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1689: XR01 - execute_graphql: Execute Custom GraphQL Query

**Module:** Xray · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Xray execute_graphql tool can run custom GraphQL queries against the Xray Cloud API.

Preconditions:
- Xray Cloud integration is configured
- API credentials are valid
- Test data exists in the target project

## Preconditions

Xray Cloud integration is configured with valid API credentials.
Test data (tests) exists in the target project.
The Xray toolkit is initialized with XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME.

## Test Data

project_key: EL (default, configurable via XRAY_PROJECT_KEY)
graphql_query: getTests with fields issueId, key, summary, testType (limit: 5)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Build a GraphQL query to retrieve up to 5 tests from the project using getTests with jql: 'project = "{project_key}"' — requesting fields: issueId, key, summary, testType (name, kind) | GraphQL query string is prepared with correct structure |
| 3 | Call `execute_graphql` tool with the prepared GraphQL query string | Tool executes without throwing an exception |
| 4 | Verify the response contains a 'data' field indicating the query ran successfully | Response includes data.getTests with total and results array |
| 5 | LLM validator checks for: tool_executed=true, no_errors=true, has_data=true, has_results=true; validates absence of error indicators | test_results: {test_passed: true, tool_executed: true, no_errors: true, has_data: true, has_results: true} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, no_errors: true, has_data: true, has_results: true}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
no_errors = true
has_data = true
has_results = true
