---
id: ELITEA-1630
title: "QT05 - update_test_case: Update Existing Test Case"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [update_test_case, happy-path, update, qtest]
requirements: []
---
# ELITEA-1630: QT05 - update_test_case: Update Existing Test Case

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest update_test_case tool updates an existing test case's fields. Tests updating status, priority and description on a pre-created test case.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Write access to the qTest project

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Original: Name='QT05 Update Test {timestamp}', Status=New, Priority=Low
Update payload: Status=Active, Priority=High, Description updated

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create prerequisite test case via create_test_cases with Name='QT05 Update Test {timestamp}', Type=Manual, Status=New, Priority=Low | Test case is created and TC- identifier is returned |
| 3 | Extract the TC- identifier from the create response | TC-xxx ID is extracted |
| 4 | Invoke update_test_case with TC-xxx and update payload: Status=Active, Priority=High, updated description | Tool executes and returns a response |
| 5 | Validate the response confirms the update with 'updated', 'success', or TC- identifier | Update confirmation received; no error indicators |
| 6 | Invoke delete_test_case with the qTest ID to clean up | Test case deleted successfully |

## Expected Final State

Test case deleted successfully

## Pass/Fail Criteria

Tool executes without errors
Response contains 'updated', 'success', or TC- confirmation
No error indicators (not found, failed, exception)
Cleanup succeeds
