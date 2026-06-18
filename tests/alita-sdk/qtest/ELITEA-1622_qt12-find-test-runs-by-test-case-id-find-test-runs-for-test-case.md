---
id: ELITEA-1622
title: "QT12 - find_test_runs_by_test_case_id: Find Test Runs for Test Case"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [find_test_runs_by_test_case_id, execution-history, happy-path, test-runs, qtest]
requirements: []
---
# ELITEA-1622: QT12 - find_test_runs_by_test_case_id: Find Test Runs for Test Case

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest find_test_runs_by_test_case_id tool finds test runs associated with a test case. Tests retrieval of execution history (test runs) for a given test case ID.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Project contains at least one test case (fallback TC-1)
Test runs may or may not exist for the selected test case

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
DQL to find test case: "Status is 'not empty'"
Fallback test_case_id: TC-1

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Search for any existing test case using search_by_dql with DQL="Status is 'not empty'" | Search returns at least one test case |
| 3 | Extract the first TC- identifier from search results (fallback to TC-1) | TC-xxx ID is available |
| 4 | Invoke find_test_runs_by_test_case_id with the extracted test_case_id | Tool executes and returns response |
| 5 | Validate the response contains 'test runs', 'TR-', 'Id', or 'Name' and no critical error indicators (excluding Status field values) | Response contains test run data or empty list; no exception or critical errors |

## Expected Final State

Response contains test run data or empty list; no exception or critical errors

## Pass/Fail Criteria

Tool executes without errors
Response contains 'test runs', TR-, Id, or Name OR indicates empty list
No exception or critical error indicators
Handles test cases with no runs gracefully
