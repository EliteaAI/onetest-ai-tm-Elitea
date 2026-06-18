---
id: ELITEA-1616
title: "QT16 - find_defects_by_test_run_id: Find Defects for Test Run"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [find_defects_by_test_run_id, happy-path, test-runs, defects, qtest]
requirements: []
---
# ELITEA-1616: QT16 - find_defects_by_test_run_id: Find Defects for Test Run

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest find_defects_by_test_run_id tool finds defects associated with a test run. Tests retrieval of defects linked to a test run ID, handling cases with no defects gracefully.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Project contains test cases with test runs (fallback TR-1)
Test runs may or may not have associated defects

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
DQL to find test case: "Id is 'not empty'"
Fallback test_run_id: TR-1

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Search for an existing test case via search_by_dql and extract its TC- ID | TC-xxx ID available |
| 3 | Use find_test_runs_by_test_case_id to get a test run ID for that test case (fallback to TR-1) | A TR-xxx test run ID is available |
| 4 | Invoke find_defects_by_test_run_id with the test run ID | Tool executes and returns response |
| 5 | Validate the response contains 'defects', 'test run', or 'Id' keywords and no error indicators; handles empty defect list gracefully | Response contains defect data or empty list; no errors |

## Expected Final State

Response contains defect data or empty list; no errors

## Pass/Fail Criteria

Tool executes without errors
Response contains 'defects', 'test run', or 'Id' OR indicates empty list
Handles test runs with no defects gracefully
No error indicators (failed, exception, not found)
