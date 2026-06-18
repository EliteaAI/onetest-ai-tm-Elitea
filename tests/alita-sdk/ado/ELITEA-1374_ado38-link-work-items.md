---
id: ELITEA-1374
title: "ADO38 - Link Work Items"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1374: ADO38 - Link Work Items

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'link_work_items' tool creates a link between two work items

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
Two work items with known IDs exist in the project.
Valid relation type name is available (from ADO37).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `link_work_items` tool with source_id, target_id, and relation_type (e.g., 'System.LinkTypes.Related') | Tool executes without error |
| 3 | Verify the response confirms the link was created between the two work items | Response contains a success confirmation or updated work item with the new relation |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
link_created = true
no_error = true
