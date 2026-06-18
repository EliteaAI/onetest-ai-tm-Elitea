---
id: ELITEA-1674
title: "TR09 - Add Cases Bulk Happy Path"
priority: high
type: functional
module: testrail
status: ready
execution_type: automated
tags: [happy-path, add_cases, testrail, create, bulk]
requirements: []
---
# ELITEA-1674: TR09 - Add Cases Bulk Happy Path

**Module:** Testrail · **Priority:** High · **Type:** Functional

**Objective:** Verify the add_cases tool creates multiple test cases in a single bulk operation. Tests bulk test case creation with full case properties including preconditions, steps and expected results.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_SECTION_ID env vars are set
Write access to the target section

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_SECTION_ID: ID of an existing section
Case 1: title='Bulk Test Case 1 - {TIMESTAMP}', template_id=1, type_id=1, priority_id=2
Case 2: title='Bulk Test Case 2 - {TIMESTAMP}', template_id=1, type_id=1, priority_id=3

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke add_cases with add_test_cases_data containing 2 case definitions: Case 1 (section_id, title='Bulk Test Case 1', template_id=1, type_id=1, priority_id=2) and Case 2 (section_id, title='Bulk Test Case 2', template_id=1, type_id=1, priority_id=3) | Tool executes successfully and creates both cases |
| 3 | Extract all created case IDs from the bulk creation response | Both case IDs are extracted as a comma-separated string |
| 4 | Invoke delete_case for each created case ID to clean up | All cases are deleted successfully |
| 5 | Validate the original add_cases response confirms creation of all specified cases with unique IDs | Response contains 2 case IDs; both cases were created successfully; no errors |

## Expected Final State

Response contains 2 case IDs; both cases were created successfully; no errors

## Pass/Fail Criteria

Tool executes successfully
Response contains IDs for all 2 created cases
Both cases are created with their respective properties
All created case IDs can be extracted
Cleanup deletion of all cases succeeds
No errors or exceptions
