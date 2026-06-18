---
id: ELITEA-1377
title: "ADO35 - Update Work Item"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1377: ADO35 - Update Work Item

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'update_work_item' tool updates an existing work item

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
A work item with a known ID exists and the test user has edit permissions.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `update_work_item` tool with the work_item_id and updated fields (e.g., new title or description) | Tool executes without error |
| 3 | Verify the response confirms the update was applied (e.g., updated field values or revision number) | Update confirmation is present in the response |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
update_confirmed = true
no_error = true
