---
id: ELITEA-1618
title: "QT11 - find_requirements_by_test_case_id: Find Linked Requirements"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [find_requirements_by_test_case_id, reverse-lookup, requirements, happy-path, qtest]
requirements: []
---
# ELITEA-1618: QT11 - find_requirements_by_test_case_id: Find Linked Requirements

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest find_requirements_by_test_case_id tool finds requirements linked to a test case. Tests reverse relationship lookup from test case to its covering requirements.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Project contains at least one test case accessible via DQL
Fallback test case ID: TC-1

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
| 4 | Invoke find_requirements_by_test_case_id with the extracted test_case_id | Tool executes and returns response |
| 5 | Validate the response contains 'requirements', 'Id', or 'Name' and no error indicators; handle empty result gracefully if no requirements linked | Response contains valid structure; handles empty requirement list without errors |

## Expected Final State

Response contains valid structure; handles empty requirement list without errors

## Pass/Fail Criteria

Tool executes without errors
Response structure is valid
Handles empty linked requirements gracefully
No error indicators (exception, not found)
