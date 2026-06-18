---
id: ELITEA-1625
title: "QT02 - get_all_test_cases_fields_for_project: Retrieve Field Definitions"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [get_all_test_cases_fields_for_project, happy-path, metadata, fields, qtest]
requirements: []
---
# ELITEA-1625: QT02 - get_all_test_cases_fields_for_project: Retrieve Field Definitions

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest get_all_test_cases_fields_for_project tool retrieves available fields and their valid values. Tests field definition retrieval including standard fields and dropdown values.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Project has standard fields configured (Status, Priority, Type)

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
force_refresh: false

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_all_test_cases_fields_for_project with project_id=QTEST_PROJECT_ID and force_refresh=false | Tool call is accepted and executes |
| 3 | Capture the fields result | Response is received and non-empty |
| 4 | Validate the result contains at least two of: 'Status', 'Priority', 'Type', 'field', 'allowed' and none of the error indicators: 'error', 'failed', 'exception', 'Unable to retrieve' | Response contains standard field definitions with allowed values; no errors present |

## Expected Final State

Response contains standard field definitions with allowed values; no errors present

## Pass/Fail Criteria

At least two expected success indicators present (Status, Priority, Type, field, allowed)
No error indicators present
Tool executed without exceptions
Field definitions present with valid values
