---
id: ELITEA-1669
title: "TR12 - Update Case Partial Update"
priority: medium
type: functional
module: testrail
status: ready
execution_type: automated
tags: [partial-update, single-field, update_case, testrail]
requirements: []
---
# ELITEA-1669: TR12 - Update Case Partial Update

**Module:** Testrail · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the update_case tool supports partial updates by modifying only a single field. Tests that updating only the estimate field leaves all other fields unchanged.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_SECTION_ID env vars are set
Write access to the target section
TestRail instance supports estimate field updates

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_SECTION_ID: ID of an existing section
Update payload: estimate='1m 30s' (only field)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Create a prerequisite test case via add_case in TESTRAIL_SECTION_ID with title '[Auto] Test Case for TR12 - Partial Update Test', template_id=1, type_id=1, priority_id=2 | Test case is created and a case ID is returned |
| 3 | Extract the numeric case ID from the add_case response | Case ID is extracted as a plain numeric string |
| 4 | Invoke update_case with case_id and case_properties containing only estimate='1m 30s' | Tool executes successfully and returns updated case data |
| 5 | Invoke delete_case with the case ID to clean up | Case is deleted successfully |
| 6 | Validate the update_case response shows the estimate field set to '1m 30s' and all originally set fields (title, priority_id, type_id) remain unchanged | Response reflects estimate='1m 30s'; other fields unchanged; no errors |

## Expected Final State

Response reflects estimate='1m 30s'; other fields unchanged; no errors

## Pass/Fail Criteria

Tool executes successfully with single field update
Response shows estimate field updated to '1m 30s'
Other fields (title, priority_id, type_id) remain unchanged
Cleanup deletion succeeds
No errors or exceptions
