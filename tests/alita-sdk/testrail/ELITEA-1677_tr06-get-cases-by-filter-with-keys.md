---
id: ELITEA-1677
title: "TR06 - Get Cases By Filter With Keys"
priority: medium
type: functional
module: testrail
status: ready
execution_type: automated
tags: [get_cases_by_filter, field-selection, testrail, keys]
requirements: []
---
# ELITEA-1677: TR06 - Get Cases By Filter With Keys

**Module:** Testrail · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the get_cases_by_filter tool supports custom field selection with the keys parameter. Tests filtering with specific field keys returned, limiting the response to only the requested fields.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_PROJECT_ID env vars are set
Project contains test cases with priority_id=2

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_PROJECT_ID: ID of an existing TestRail project
json_case_arguments: {\"priority_id\": 2}
output_format: json
keys: [\"id\", \"title\", \"priority_id\"]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_cases_by_filter with project_id=TESTRAIL_PROJECT_ID, json_case_arguments='{"priority_id": 2}', output_format='json', and keys=['id','title','priority_id'] | Tool call is accepted and executes |
| 3 | Capture the tool response | Response is received and is non-empty |
| 4 | Validate the response objects contain only the specified keys (id, title, priority_id) and no additional fields | Each test case object in the response has exactly the fields id, title, and priority_id; no other fields present; no errors |

## Expected Final State

Each test case object in the response has exactly the fields id, title, and priority_id; no other fields present; no errors

## Pass/Fail Criteria

Tool executes successfully with keys parameter
Returned test case objects contain only the specified fields: id, title, priority_id
Other fields are absent from the response objects
Filter criteria (priority_id=2) is applied correctly
No errors or exceptions
