---
id: ELITEA-1672
title: "TR11 - Update Case Happy Path"
priority: high
type: functional
module: testrail
status: ready
execution_type: automated
tags: [update_case, happy-path, testrail, update]
requirements: []
---
# ELITEA-1672: TR11 - Update Case Happy Path

**Module:** Testrail · **Priority:** High · **Type:** Functional

**Objective:** Verify the update_case tool updates an existing test case. Tests updating multiple case properties (title, priority_id) on a pre-created test case.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_SECTION_ID env vars are set
Write access to the target section

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_SECTION_ID: ID of an existing section
Update payload: title='Updated Test Case Title', priority_id=4

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create a prerequisite test case via add_case in TESTRAIL_SECTION_ID with title '[Auto] Test Case for TR11 - Update Case Test', template_id=1, type_id=1, priority_id=2 | Test case is created and a case ID is returned |
| 3 | Extract the numeric case ID from the add_case response | Case ID is extracted as a plain numeric string |
| 4 | Invoke update_case with the extracted case_id and case_properties: title='Updated Test Case Title', priority_id=4 | Tool executes successfully and returns updated case data |
| 5 | Invoke delete_case with the case ID to clean up | Case is deleted successfully |
| 6 | Validate the update_case response shows updated title 'Updated Test Case Title' and priority_id=4 | Response reflects the new title and priority_id values; updated_on timestamp is present; no errors |

## Expected Final State

Response reflects the new title and priority_id values; updated_on timestamp is present; no errors

## Pass/Fail Criteria

Tool executes successfully
Response reflects the updated title 'Updated Test Case Title'
Response reflects the updated priority_id=4
Updated timestamp is returned
Cleanup deletion succeeds
No errors or exceptions
