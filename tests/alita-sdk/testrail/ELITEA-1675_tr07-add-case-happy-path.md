---
id: ELITEA-1675
title: "TR07 - Add Case Happy Path"
priority: high
type: functional
module: testrail
status: ready
execution_type: automated
tags: [happy-path, add_case, testrail, create]
requirements: []
---
# ELITEA-1675: TR07 - Add Case Happy Path

**Module:** Testrail · **Priority:** High · **Type:** Functional

**Objective:** Verify the add_case tool creates a new test case with basic properties. Tests creating a new test case with title, section, template, type, priority, preconditions, steps and expected result fields.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_SECTION_ID env vars are set
Write access to the target section

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_SECTION_ID: ID of an existing section
Title: Automated Test Case - TR07 - {TIMESTAMP}
case_properties: template_id=1, type_id=1, priority_id=2, custom_preconds='Test preconditions', custom_steps='Test steps', custom_expected='Expected result'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke add_case with section_id=TESTRAIL_SECTION_ID, title='Automated Test Case - TR07 - {TIMESTAMP}', and case_properties: template_id=1, type_id=1, priority_id=2, custom_preconds='Test preconditions', custom_steps='Test steps', custom_expected='Expected result' | Tool executes successfully and returns a response containing a case ID |
| 3 | Extract the numeric case ID from the add_case response | Case ID is extracted as a plain numeric string |
| 4 | Invoke delete_case with the extracted case ID to clean up | Case is deleted successfully (soft delete) |
| 5 | Validate the original add_case response confirms case creation with a valid ID and timestamp | Response contains numeric case ID and indicates successful creation; no errors |

## Expected Final State

Response contains numeric case ID and indicates successful creation; no errors

## Pass/Fail Criteria

Tool executes successfully
Response contains a valid numeric case ID
Case is created in the specified section
All provided properties (template_id, type_id, priority_id, preconditions, steps, expected) are saved
Cleanup deletion succeeds
No errors or exceptions
