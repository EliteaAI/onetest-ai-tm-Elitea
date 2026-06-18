---
id: ELITEA-1690
title: "XR05 - get_test_step_attachments: Retrieve Test Step Attachments"
priority: medium
type: functional
module: xray
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1690: XR05 - get_test_step_attachments: Retrieve Test Step Attachments

**Module:** Xray · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Xray get_test_step_attachments tool retrieves attachment metadata from test steps.

Preconditions:
- Xray Cloud integration is configured
- Manual tests with steps exist in the project (labeled ELITEA_AI_CREATED)

## Preconditions

Xray Cloud integration is configured with valid API credentials.
Manual tests with label ELITEA_AI_CREATED exist in the project.
The Xray toolkit is initialized.

## Test Data

jql_query: "labels in (ELITEA_AI_CREATED) ORDER BY assignee"
issue_id: dynamically extracted from get_tests result (first matching test's issueId)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Call `get_tests` tool with JQL: 'labels in (ELITEA_AI_CREATED) ORDER BY assignee' to fetch existing tests | List of tests is returned with issueId values |
| 3 | Extract the issueId of the first test from the get_tests result using regex (looking for 'issueId' numeric or key format) | A valid test_issue_id is extracted |
| 4 | Call `get_test_step_attachments` tool with the extracted issue_id parameter | Tool executes without throwing an exception |
| 5 | LLM validator checks: tool_executed=true, no_errors=true, valid_response=true, test_id_valid=true. Note: 'No attachments found' is still a PASS as long as no errors occur | test_results: {test_passed: true, tool_executed: true, no_errors: true, valid_response: true, test_id_valid: true} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, no_errors: true, valid_response: true, test_id_valid: true}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
no_errors = true (note: 'No attachments found' is NOT an error)
valid_response = true
test_id_valid = true
