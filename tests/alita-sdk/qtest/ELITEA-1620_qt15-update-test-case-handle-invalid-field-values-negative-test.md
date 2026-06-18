---
id: ELITEA-1620
title: "QT15 - update_test_case: Handle Invalid Field Values (Negative Test)"
priority: medium
type: functional
module: qtest
status: ready
execution_type: automated
tags: [update_test_case, error-handling, negative-test, validation, qtest]
requirements: []
---
# ELITEA-1620: QT15 - update_test_case: Handle Invalid Field Values (Negative Test)

**Module:** Qtest · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the qTest update_test_case tool properly handles invalid field values. Tests error handling when updating a test case with non-existent field values that fail validation.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Project contains at least one test case (located via DQL search)

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
DQL to find test case: "Status is 'not empty'"
Invalid update payload: field values not in allowed list (e.g. Status='INVALID_STATUS_XYZ')

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Search for any existing test case using search_by_dql with DQL="Status is 'not empty'" to get a valid TC- ID | A TC-xxx ID is retrieved |
| 3 | Extract the TC- identifier from search results | TC-xxx ID available |
| 4 | Invoke update_test_case with the TC- ID and invalid field values (e.g. Status='INVALID_STATUS_XYZ') | Tool executes without crashing |
| 5 | Validate the response DOES contain error indicators ('error', 'invalid', 'not allowed', 'validation', 'failed') and DOES NOT contain success indicators ('successfully', 'updated', 'modified') | Validation error returned; test case not modified; no crash |

## Expected Final State

Validation error returned; test case not modified; no crash

## Pass/Fail Criteria

Tool was called (executed)
Response contains error indicator (error, invalid, not allowed, validation, failed)
No success indicators (successfully, updated, modified)
Tool did not crash
