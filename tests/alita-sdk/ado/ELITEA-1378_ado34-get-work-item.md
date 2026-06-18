---
id: ELITEA-1378
title: "ADO34 - Get Work Item"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1378: ADO34 - Get Work Item

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_work_item' tool retrieves work item details by ID

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
A work item with a known ID exists in the project.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_work_item` tool with a known work_item_id | Tool executes without error |
| 3 | Verify the response contains the work item ID matching the requested ID | Returned ID matches the requested work item ID |
| 4 | Verify the response includes key fields: title, type, and state | Title, type, and state fields are present in the response |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
work_item_details_present = true
no_error = true
