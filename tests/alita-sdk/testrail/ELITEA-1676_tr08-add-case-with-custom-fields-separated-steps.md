---
id: ELITEA-1676
title: "TR08 - Add Case With Custom Fields (Separated Steps)"
priority: medium
type: functional
module: testrail
status: ready
execution_type: automated
tags: [separated-steps, custom-fields, template, add_case, testrail]
requirements: []
---
# ELITEA-1676: TR08 - Add Case With Custom Fields (Separated Steps)

**Module:** Testrail · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the add_case tool supports custom fields using template_id=2 (separated steps format). Tests creating a test case with custom_steps_separated containing individual step/expected pairs.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_SECTION_ID env vars are set
Write access to the target section
TestRail instance supports template_id=2

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_SECTION_ID: ID of an existing section
Title: Automated Test Case - TR08 - {TIMESTAMP}
case_properties: template_id=2, type_id=1, priority_id=3, custom_preconds='Advanced test preconditions', custom_steps_separated=[{content,expected},{content,expected}]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke add_case with section_id=TESTRAIL_SECTION_ID, title='Automated Test Case - TR08 - {TIMESTAMP}', and case_properties: template_id=2, type_id=1, priority_id=3, custom_preconds='Advanced test preconditions', custom_steps_separated=[{content: 'Step 1 description', expected: 'Step 1 expected result'},{content: 'Step 2 description', expected: 'Step 2 expected result'}] | Tool executes successfully and returns a response containing a case ID |
| 3 | Extract the numeric case ID from the add_case response | Case ID is extracted as a plain numeric string |
| 4 | Invoke delete_case with the extracted case ID to clean up | Case is deleted successfully |
| 5 | Validate the original add_case response confirms case creation with proper separated steps format | Response contains case ID; case was created with template_id=2 and custom_steps_separated stored correctly; no errors |

## Expected Final State

Response contains case ID; case was created with template_id=2 and custom_steps_separated stored correctly; no errors

## Pass/Fail Criteria

Tool executes successfully with template_id=2
Response contains a valid case ID
Case is created with separated steps format
custom_steps_separated field is saved with step content and expected pairs
Cleanup deletion succeeds
No errors or exceptions
