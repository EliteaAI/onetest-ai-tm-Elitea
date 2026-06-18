---
id: ELITEA-1632
title: "QT03 - create_test_cases: Create a New Test Case"
priority: critical
type: functional
module: qtest
status: ready
execution_type: automated
tags: [create_test_cases, happy-path, create, qtest]
requirements: []
---
# ELITEA-1632: QT03 - create_test_cases: Create a New Test Case

**Module:** Qtest · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the qTest create_test_cases tool creates a new test case with steps. Tests creation of a manual test case with name, description, status, priority, preconditions and multiple test steps.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Write access to the qTest project

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Test case: Name='QT03 Automated Test {timestamp}', Type='Manual', Status='New', Priority='High', with 3 steps

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Prepare test case data with unique name, Type=Manual, Status=New, Priority=High, Precondition, and 3 numbered steps (login flow) | Test case JSON is prepared with all required fields |
| 3 | Invoke create_test_cases with the prepared test case JSON | Tool executes successfully and returns a response |
| 4 | Validate the response contains TC- identifier and creation confirmation with Id and QTest Id fields | Response contains valid TC-xxx identifier indicating successful creation |
| 5 | Invoke delete_test_case with the created qTest ID to clean up | Test case is deleted successfully |

## Expected Final State

Test case is deleted successfully

## Pass/Fail Criteria

Tool executes without errors
Response contains TC- format identifier
Response contains created/Id/QTest Id fields
Cleanup deletion succeeds
No error indicators
