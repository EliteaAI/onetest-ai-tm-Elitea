---
id: ELITEA-1626
title: "QT09 - delete_test_case: Delete Test Case"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [delete_test_case, happy-path, cleanup, delete, qtest]
requirements: []
---
# ELITEA-1626: QT09 - delete_test_case: Delete Test Case

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest delete_test_case tool successfully deletes a test case by its qTest ID. Tests the full delete flow: create, delete, and verify the case no longer exists.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Write access to the qTest project

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Test case: Name='QT09 Test for Deletion {timestamp}', Type=Manual, Status=New, Priority=Low, 1 step

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create a test case via create_test_cases with Name='QT09 Test for Deletion {timestamp}' | Test case created; TC- and qTest numeric ID returned |
| 3 | Extract the numeric qTest ID from create response | qTest numeric ID extracted |
| 4 | Invoke delete_test_case with the extracted qTest ID | Tool executes and returns response |
| 5 | Validate the delete response contains 'deleted', 'successfully', or 'removed' | Deletion confirmed with success message; no error indicators |
| 6 | Attempt find_test_case_by_id with the original TC- ID to verify it no longer exists | Response returns 0 results or not found, confirming deletion |

## Expected Final State

Response returns 0 results or not found, confirming deletion

## Pass/Fail Criteria

Delete tool executes without errors
Response contains 'deleted', 'successfully', or 'removed'
Subsequent lookup returns empty/not found
No error indicators (Unable to delete, exception)
