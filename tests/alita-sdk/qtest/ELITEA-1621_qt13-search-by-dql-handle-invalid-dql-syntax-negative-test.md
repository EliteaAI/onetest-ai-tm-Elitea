---
id: ELITEA-1621
title: "QT13 - search_by_dql: Handle Invalid DQL Syntax (Negative Test)"
priority: medium
type: functional
module: qtest
status: ready
execution_type: automated
tags: [error-handling, search_by_dql, negative-test, invalid-dql, qtest]
requirements: []
---
# ELITEA-1621: QT13 - search_by_dql: Handle Invalid DQL Syntax (Negative Test)

**Module:** Qtest · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the qTest search_by_dql tool properly handles malformed DQL queries. Tests error handling for invalid DQL syntax — expects an error response, not test case data.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
Invalid DQL: "Status = AND Priority INVALID ((("

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke search_by_dql with malformed DQL: "Status = AND Priority INVALID (((" | Tool is called and returns a response without crashing |
| 3 | Capture the search result | Response received (error response expected) |
| 4 | Validate the response DOES contain error indicators ('error', 'Invalid DQL', 'syntax', 'parse', 'failed') and DOES NOT contain success indicators ('TC-', 'found', 'results') | Error message present indicating bad DQL syntax; no test case data returned; tool did not crash |

## Expected Final State

Error message present indicating bad DQL syntax; no test case data returned; tool did not crash

## Pass/Fail Criteria

Tool was called (executed)
Response contains error indicator (error, Invalid DQL, syntax, parse, failed)
No success indicators present (TC-, found, results)
Tool did not raise unhandled exception
