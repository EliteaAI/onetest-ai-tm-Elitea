---
id: ELITEA-1376
title: "ADO36 - Get Work Item Type Fields"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1376: ADO36 - Get Work Item Type Fields

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_work_item_type_fields' tool retrieves field definitions for a work item type

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
Work item type (e.g., 'Task' or 'Bug') exists in the project.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_work_item_type_fields` tool with a work item type name (e.g., 'Task') | Tool executes without error |
| 3 | Verify the response contains a list of field definitions | Response is a non-empty list of field objects |
| 4 | Verify each field entry contains field name and type information | Field entries include identifiable metadata (name, type) |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
fields_returned = true
no_error = true
