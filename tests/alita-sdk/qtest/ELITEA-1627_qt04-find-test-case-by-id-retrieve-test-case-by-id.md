---
id: ELITEA-1627
title: "QT04 - find_test_case_by_id: Retrieve Test Case by ID"
priority: critical
type: functional
module: qtest
status: ready
execution_type: automated
tags: [find_test_case_by_id, happy-path, qtest, read]
requirements: []
---
# ELITEA-1627: QT04 - find_test_case_by_id: Retrieve Test Case by ID

**Module:** Qtest · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the qTest find_test_case_by_id tool retrieves a test case by its ID. Tests retrieval of a specific test case using its TC- identifier. Depends on creating a test case as prerequisite.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
A test case is created during the test as prerequisite

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Prerequisite test case: Name='QT04 Find Test {timestamp}', Type=Manual, Status=New, Priority=Medium

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create prerequisite test case via create_test_cases with Name='QT04 Find Test {timestamp}', Type=Manual, Status=New, Priority=Medium | Test case is created and a TC- identifier is returned |
| 3 | Extract the TC- identifier from the create response | TC-xxx ID is extracted successfully |
| 4 | Invoke find_test_case_by_id with test_id=<extracted TC-xxx> | Tool executes and returns a response |
| 5 | Validate the response contains TC- Id, Name, Description, and QTest Id fields | Full test case details returned matching the created case |
| 6 | Invoke delete_test_case with the qTest ID to clean up | Test case deleted successfully |

## Expected Final State

Test case deleted successfully

## Pass/Fail Criteria

Tool executes without errors
Response contains TC- identifier, Name, Description, QTest Id
Returned data matches the created test case
Cleanup succeeds
No error indicators
