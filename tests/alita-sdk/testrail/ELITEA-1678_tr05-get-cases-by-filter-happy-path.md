---
id: ELITEA-1678
title: "TR05 - Get Cases By Filter Happy Path"
priority: high
type: functional
module: testrail
status: ready
execution_type: automated
tags: [get_cases_by_filter, happy-path, testrail, filter]
requirements: []
---
# ELITEA-1678: TR05 - Get Cases By Filter Happy Path

**Module:** Testrail · **Priority:** High · **Type:** Functional

**Objective:** Verify the get_cases_by_filter tool retrieves test cases using filter criteria. Tests filtering test cases by specific attributes such as type_id.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_PROJECT_ID env vars are set
Project contains test cases with type_id=1

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_PROJECT_ID: ID of an existing TestRail project
json_case_arguments: {\"type_id\": 1}
output_format: json

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_cases_by_filter with project_id=TESTRAIL_PROJECT_ID, json_case_arguments='{"type_id": 1}', and output_format='json' | Tool call is accepted and executes |
| 3 | Capture the tool response | Response is received and is non-empty |
| 4 | Validate the response contains test case data matching the filter criteria (type_id=1) | Response contains JSON list of test cases that match the type_id=1 filter; each result has type_id=1; no errors present |

## Expected Final State

Response contains JSON list of test cases that match the type_id=1 filter; each result has type_id=1; no errors present

## Pass/Fail Criteria

Tool executes successfully with filter parameters
Returned cases match the filter criteria (type_id=1)
Response is in JSON format
No errors or exceptions
