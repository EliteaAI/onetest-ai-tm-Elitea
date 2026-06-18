---
id: ELITEA-1682
title: "TR01 - Get Case Happy Path"
priority: high
type: functional
module: testrail
status: ready
execution_type: automated
tags: [happy-path, get_case, testrail, read]
requirements: []
---
# ELITEA-1682: TR01 - Get Case Happy Path

**Module:** Testrail · **Priority:** High · **Type:** Functional

**Objective:** Verify the get_case tool retrieves information about a single test case from TestRail. Tests basic retrieval of test case details by ID using a pre-created case.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_SECTION_ID env vars are set
Write access to the target TestRail project

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_TOOLKIT_ID: ID of the toolkit configuration
TESTRAIL_SECTION_ID: ID of an existing section where the test case will be created

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create a prerequisite test case via add_case in TESTRAIL_SECTION_ID with title '[Auto] Test Case for TR01 - Get Case Test' and template_id=1, type_id=1, priority_id=2 | Test case is created successfully and a case ID is returned |
| 3 | Extract the numeric case ID from the add_case response | Case ID is extracted as a plain numeric string |
| 4 | Invoke get_case tool with the extracted case ID as testcase_id | Tool executes successfully with no errors |
| 5 | Validate the returned case data contains fields including id and title | Response includes case details: id matches the created case, title is present and non-empty |

## Expected Final State

Response includes case details: id matches the created case, title is present and non-empty

## Pass/Fail Criteria

Tool executes successfully with valid case ID
Returned object contains id field matching the queried case
Returned object contains title field
No errors or exceptions in response
