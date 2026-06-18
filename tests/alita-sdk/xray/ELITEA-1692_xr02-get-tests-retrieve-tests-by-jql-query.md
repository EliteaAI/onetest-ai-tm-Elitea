---
id: ELITEA-1692
title: "XR02 - get_tests: Retrieve Tests by JQL Query"
priority: high
type: functional
module: xray
status: passed
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1692: XR02 - get_tests: Retrieve Tests by JQL Query

**Module:** Xray · **Priority:** High · **Type:** Functional

**Objective:** Verify the Xray get_tests tool retrieves tests using JQL (JIRA Query Language) queries.

Preconditions:
- Xray Cloud integration is configured
- Tests exist with the label 'ELITEA_AI_CREATED'
- Valid JQL syntax is used

## Preconditions

Xray Cloud integration is configured with valid API credentials.
Tests with label 'ELITEA_AI_CREATED' exist in the project.
The Xray toolkit is initialized with XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME.

## Test Data

jql_query: "labels in (ELITEA_AI_CREATED) ORDER BY assignee"
project_key: EL

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Prepare JQL query: 'labels in (ELITEA_AI_CREATED) ORDER BY assignee' | JQL query string is ready |
| 3 | Call `get_tests` tool with the JQL query via the `jql` parameter | Tool executes without throwing an exception |
| 4 | Verify the response contains 'Extracted tests' with a count and test detail fields (issueId, jira key/summary) | Response lists tests matching the JQL filter |
| 5 | LLM validator checks: tool_executed=true, no_errors=true, has_extracted_tests=true, has_test_data=true | test_results: {test_passed: true, tool_executed: true, no_errors: true, has_extracted_tests: true, has_test_data: true, tests_count: >=1} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, no_errors: true, has_extracted_tests: true, has_test_data: true, tests_count: >=1}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
no_errors = true
has_extracted_tests = true
has_test_data = true
