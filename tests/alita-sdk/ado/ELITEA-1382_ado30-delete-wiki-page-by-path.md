---
id: ELITEA-1382
title: "ADO30 - Delete Wiki Page by Path"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [toolkit, wiki, sdk, ado]
requirements: []
---
# ELITEA-1382: ADO30 - Delete Wiki Page by Path

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'delete_page_by_path' tool deletes a wiki page using its path

## Preconditions

ADO Wiki toolkit is configured with valid credentials.
Target wiki page exists at the specified path.
Test user has write permissions on the wiki.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Wiki toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `delete_page_by_path` tool with the wiki identifier and the page path to delete | Tool executes without error |
| 3 | Verify the response confirms the page was deleted (e.g., HTTP 204, 'deleted', or empty success response) | Deletion confirmation is present |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
page_deleted = true
no_error = true
