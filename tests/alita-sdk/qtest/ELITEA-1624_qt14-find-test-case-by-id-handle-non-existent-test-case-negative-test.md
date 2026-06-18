---
id: ELITEA-1624
title: "QT14 - find_test_case_by_id: Handle Non-Existent Test Case (Negative Test)"
priority: medium
type: functional
module: qtest
status: ready
execution_type: automated
tags: [find_test_case_by_id, error-handling, negative-test, nonexistent, qtest]
requirements: []
---
# ELITEA-1624: QT14 - find_test_case_by_id: Handle Non-Existent Test Case (Negative Test)

**Module:** Qtest · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the qTest find_test_case_by_id tool properly handles requests for non-existent test cases. Tests that querying TC-999999999 returns empty result, not an error crash.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Test case TC-999999999 does not exist in the project

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Non-existent test ID: TC-999999999

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke find_test_case_by_id with test_id=TC-999999999 | Tool executes without crashing |
| 3 | Capture the find result | Response received |
| 4 | Validate the response indicates empty result: 'Found 0', '[]', or 'empty', and DOES NOT contain test case data fields like 'QTest Id', 'Name', 'Description', 'Steps' | Response shows 0 results or empty list; no test case data returned; graceful handling |

## Expected Final State

Response shows 0 results or empty list; no test case data returned; graceful handling

## Pass/Fail Criteria

Tool was called (executed)
Response indicates 0 results, empty, or [] 
No test case data fields returned (QTest Id, Name, Description, Steps)
Tool did not crash
