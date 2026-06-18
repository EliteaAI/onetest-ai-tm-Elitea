---
id: ELITEA-1380
title: "ADO32 - Search Work Items"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1380: ADO32 - Search Work Items

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'search_work_items' tool retrieves work items using WIQL query

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
Work items exist in the project that match the test WIQL query.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `search_work_items` tool with a WIQL query (e.g., SELECT * FROM WorkItems WHERE [System.TeamProject] = '@project') | Tool executes without error |
| 3 | Verify the response contains a list of work items | Result is a non-empty list or array with work item objects |
| 4 | Verify each work item entry has basic identifying fields (e.g., ID, title, or type) | Work item entries contain identifiable metadata |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
work_items_returned = true
no_error = true
