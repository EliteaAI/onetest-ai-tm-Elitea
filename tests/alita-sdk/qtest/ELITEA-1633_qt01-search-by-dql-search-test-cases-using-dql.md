---
id: ELITEA-1633
title: "QT01 - search_by_dql: Search Test Cases Using DQL"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [search_by_dql, happy-path, search, qtest, dql]
requirements: []
---
# ELITEA-1633: QT01 - search_by_dql: Search Test Cases Using DQL

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest search_by_dql tool searches for test cases using Data Query Language (DQL). Tests DQL-based search for retrieving test cases with status filtering.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_ID, QTEST_TOOLKIT_NAME, and QTEST_PROJECT_ID env vars are set
Project contains test cases with Status = 'New' or 'Active'

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
dql_query: "Status = 'New' or Status = 'Active'"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke search_by_dql with dql="Status = 'New' or Status = 'Active'" | Tool accepts the DQL query and executes |
| 3 | Capture the search result | Response is received and non-empty |
| 4 | Validate the result contains expected success indicators: 'TC-', 'Id', 'Name' and none of the error indicators: 'error', 'failed', 'exception', 'Invalid DQL', 'syntax error' | Response contains at least one success indicator; no error indicators present; test case data is returned |

## Expected Final State

Response contains at least one success indicator; no error indicators present; test case data is returned

## Pass/Fail Criteria

At least one expected success indicator (TC-, Id, Name) is present
No error indicators present
Tool executed without exceptions
Test case data structure is returned
