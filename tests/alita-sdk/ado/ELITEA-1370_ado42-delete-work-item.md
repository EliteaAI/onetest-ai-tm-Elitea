---
id: ELITEA-1370
title: "ADO42 - Delete Work Item"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1370: ADO42 - Delete Work Item

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'delete_work_item' tool deletes a work item by ID

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
A work item with a known ID exists in the project.
Test user has delete permissions for work items.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Identify the work_item_id to delete (from test state variables) | Valid work_item_id is available |
| 2 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 3 | Call `delete_work_item` tool with the target work_item_id | Tool executes without error |
| 4 | Verify the response confirms the work item was deleted | Response contains success/deletion confirmation |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |
| 6 | LLM validator evaluates the result and confirms test_passed=true, work_item_deleted=true | Structured test_results: {test_passed: true, tool_executed: true, work_item_deleted: true, no_error: true} |

## Expected Final State

Structured test_results: {test_passed: true, tool_executed: true, work_item_deleted: true, no_error: true}

## Pass/Fail Criteria

test_passed = true
tool_executed = true
work_item_deleted = true
no_error = true
