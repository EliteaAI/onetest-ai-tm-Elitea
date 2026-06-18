---
id: ELITEA-1679
title: "TR02 - Get Case Error Handling"
priority: medium
type: functional
module: testrail
status: ready
execution_type: automated
tags: [error-handling, negative-test, get_case, testrail]
requirements: []
---
# ELITEA-1679: TR02 - Get Case Error Handling

**Module:** Testrail · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the get_case tool handles invalid test case IDs gracefully. Tests error handling for a non-existent test case.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME and TESTRAIL_TOOLKIT_ID env vars are set
Case ID 999999999 does not exist in the TestRail instance

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_TOOLKIT_ID: ID of the toolkit configuration
testcase_id: 999999999 (intentionally invalid/non-existent ID)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_case tool with testcase_id=999999999 (non-existent case ID) | Tool executes without crashing or throwing unhandled exception |
| 3 | Capture the full tool response | Response is received (not empty or null) |
| 4 | Validate the error message content indicates an invalid or missing case | Response contains expected error pattern such as 'case does not exist', 'not found', 'invalid case id', HTTP 404 or HTTP 400 error |

## Expected Final State

Response contains expected error pattern such as 'case does not exist', 'not found', 'invalid case id', HTTP 404 or HTTP 400 error

## Pass/Fail Criteria

Tool does not crash or throw unhandled exception
Response is not empty
Error message references the invalid case ID or indicates not found
HTTP 404 or 400 is acceptable; system-level errors are failures
