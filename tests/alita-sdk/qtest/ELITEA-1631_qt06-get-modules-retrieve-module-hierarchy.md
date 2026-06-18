---
id: ELITEA-1631
title: "QT06 - get_modules: Retrieve Module Hierarchy"
priority: high
type: functional
module: qtest
status: ready
execution_type: automated
tags: [get_modules, happy-path, hierarchy, modules, qtest]
requirements: []
---
# ELITEA-1631: QT06 - get_modules: Retrieve Module Hierarchy

**Module:** Qtest · **Priority:** High · **Type:** Functional

**Objective:** Verify the qTest get_modules tool retrieves the module/folder structure for organizing test cases. Tests retrieval of the full module hierarchy with id, name and path information.

## Preconditions

qTest toolkit is configured and authenticated
QTEST_TOOLKIT_NAME and QTEST_PROJECT_ID env vars are set
Project has at least one module/folder configured

## Test Data

QTEST_TOOLKIT_NAME: name of configured qTest toolkit
QTEST_PROJECT_ID: ID of existing qTest project
parent_id: null (root level)
search: null

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the qTest toolkit using QTEST_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke get_modules with project_id=QTEST_PROJECT_ID, parent_id=null, search=null | Tool call is accepted and executes |
| 3 | Capture the modules result | Response is received |
| 4 | Validate the result contains 'Found', 'module' and module data with 'id':, 'name': keys OR 'No modules found' message, and none of the error indicators | Response contains module hierarchy data or indicates empty modules; no errors |

## Expected Final State

Response contains module hierarchy data or indicates empty modules; no errors

## Pass/Fail Criteria

Response contains 'Found' and 'module' keywords OR 'No modules found'
Module data contains 'id': and 'name': keys if modules exist
No error indicators present
Tool executed without exceptions
