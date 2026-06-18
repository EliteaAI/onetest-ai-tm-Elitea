---
id: ELITEA-1375
title: "ADO37 - Get Relation Types"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, sdk, ado]
requirements: []
---
# ELITEA-1375: ADO37 - Get Relation Types

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_relation_types' tool retrieves available work item link types

## Preconditions

ADO Work Items toolkit is configured with valid credentials.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_relation_types` tool with no additional parameters | Tool executes without error |
| 3 | Verify the response contains a list of relation/link types | Response is a non-empty list of relation type objects |
| 4 | Verify at least common relation types are present (e.g., 'Parent', 'Child', or 'Related') | Known relation type names appear in the results |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
relation_types_returned = true
no_error = true
