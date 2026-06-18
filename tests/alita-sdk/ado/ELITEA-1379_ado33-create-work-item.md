---
id: ELITEA-1379
title: "ADO33 - Create Work Item"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1379: ADO33 - Create Work Item

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'create_work_item' tool creates a new work item

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
Test user has permission to create work items in the project.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `create_work_item` tool with work_item_type (e.g., 'Task'), title, and description | Tool executes without error |
| 3 | Verify the response contains a new work item ID | Response includes a numeric work item ID |
| 4 | Verify the response confirms creation with title and type fields | Created work item has the specified title and type |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
work_item_created = true
new_id_returned = true
no_error = true
