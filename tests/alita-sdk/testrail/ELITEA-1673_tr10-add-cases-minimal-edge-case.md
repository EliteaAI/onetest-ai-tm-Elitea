---
id: ELITEA-1673
title: "TR10 - Add Cases Minimal (Edge Case)"
priority: medium
type: functional
module: testrail
status: ready
execution_type: automated
tags: [minimal-input, add_cases, edge-case, testrail, defaults]
requirements: []
---
# ELITEA-1673: TR10 - Add Cases Minimal (Edge Case)

**Module:** Testrail · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the add_cases tool handles bulk creation with minimal case data (empty case_properties). Tests edge case where only required fields are provided and defaults are applied.

## Preconditions

TestRail toolkit is configured and authenticated
TESTRAIL_TOOLKIT_NAME, TESTRAIL_TOOLKIT_ID, and TESTRAIL_SECTION_ID env vars are set
Write access to the target section

## Test Data

TESTRAIL_TOOLKIT_NAME: name of configured TestRail toolkit
TESTRAIL_SECTION_ID: ID of an existing section
Case: title='Minimal Test Case - {TIMESTAMP}', case_properties={} (empty)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the TestRail toolkit using TESTRAIL_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke add_cases with add_test_cases_data containing a single case definition using only required fields: section_id=TESTRAIL_SECTION_ID, title='Minimal Test Case - {TIMESTAMP}', and empty case_properties={} | Tool call is accepted and executes without validation errors |
| 3 | Extract the created case ID from the response | Case ID is extracted as a plain numeric string |
| 4 | Invoke delete_case with the extracted case ID (soft_delete=true) to clean up | Case is deleted successfully |
| 5 | Validate the add_cases response confirms case creation with default values applied | Response contains a case ID; case was created with TestRail defaults for unspecified fields; no errors |

## Expected Final State

Response contains a case ID; case was created with TestRail defaults for unspecified fields; no errors

## Pass/Fail Criteria

Tool executes successfully with minimal input
Response contains at least one case ID
Case is created with TestRail default values applied
Cleanup deletion succeeds
No errors or exceptions thrown due to missing optional fields
