---
id: ELITEA-1684
title: "XR10 - get_tests: Handle Invalid JQL Syntax (Negative Test)"
priority: medium
type: functional
module: xray
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1684: XR10 - get_tests: Handle Invalid JQL Syntax (Negative Test)

**Module:** Xray · **Priority:** Medium · **Type:** Functional

**Objective:** NEGATIVE TEST: Verify proper error handling when get_tests receives malformed JQL syntax.

Preconditions:
- Xray Cloud integration is configured
- System properly validates JQL syntax before/during API call

## Preconditions

Xray Cloud integration is configured with valid API credentials.
The tool validates JQL before or during API call and returns an error on invalid syntax.
This is a NEGATIVE test — the expected outcome is a proper error response, not test data.

## Test Data

invalid_jql_query: "project = AND testType INVALID SYNTAX (((  — intentionally broken JQL with missing value and unmatched parentheses)
project_key: EL (configurable via XRAY_PROJECT_KEY)
expected_error_indicators: ["Unable to get tests", "error", "failed", "exception", "syntax", "parse"]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure Xray Cloud toolkit using XRAY_TOOLKIT_ID and XRAY_TOOLKIT_NAME | Toolkit initialized successfully |
| 2 | Prepare intentionally malformed JQL query: 'project = AND testType INVALID SYNTAX (((' (broken syntax with missing value and unmatched parentheses) | Invalid JQL string is set |
| 3 | Call `get_tests` tool with the malformed JQL via the `jql` parameter (note: continue_on_error=true so the pipeline does not halt) | Tool returns an error response instead of crashing the pipeline |
| 4 | Verify the error response is non-empty (length > 10 chars) and contains error keywords such as 'Unable to get tests', 'error', 'failed', 'syntax', or 'parse' | Error message is meaningful and references the JQL parsing problem |
| 5 | LLM validator verifies negative test criteria: has_error_message=true, error_message_meaningful=true, no_test_data=true (no issueId/jira references), no_success_message=true (no 'Extracted tests' phrase) | test_results: {test_passed: true, tool_executed: true, has_error_message: true, error_message_meaningful: true, no_test_data: true, no_success_message: true} |

## Expected Final State

test_results: {test_passed: true, tool_executed: true, has_error_message: true, error_message_meaningful: true, no_test_data: true, no_success_message: true}

## Pass/Fail Criteria

test_passed = true (NEGATIVE test — error handling is working)
tool_executed = true
has_error_message = true (result length > 10 chars)
error_message_meaningful = true (contains: "Unable to get tests", "error", "failed", "syntax", or "parse")
no_test_data = true (no issueId/jira fields)
no_success_message = true (no "Extracted tests")
