---
id: ELITEA-1385
title: "ADO27 - Get Wiki"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [toolkit, wiki, sdk, ado]
requirements: []
---
# ELITEA-1385: ADO27 - Get Wiki

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'get_wiki' tool retrieves wiki information

## Preconditions

ADO Wiki toolkit is configured with valid credentials.
ADO_WIKI_TOOLKIT_ID and ADO_WIKI_TOOLKIT_NAME are set.
At least one wiki exists in the ADO project.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Wiki toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_wiki` tool | Tool executes without error |
| 3 | Verify the response contains wiki metadata (e.g., wiki name, ID, type, or project info) | Wiki information is present in the response |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
wiki_info_returned = true
no_error = true
