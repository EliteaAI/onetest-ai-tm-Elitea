---
id: ELITEA-1406
title: "ADO06 - Get Work Items for Pull Request"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [pull-requests, work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1406: ADO06 - Get Work Items for Pull Request

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_work_items' tool returns work item IDs associated with a pull request

## Preconditions

ADO Repos toolkit is configured with valid credentials.
Pull request #10 exists and has linked work items.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Repos toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_work_items` tool with pull_request_id = '10' | Tool executes without error |
| 3 | Verify the response contains work item IDs or a valid structure | Result is a non-empty list or object with work item data |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
work items list is non-empty or has valid structure
