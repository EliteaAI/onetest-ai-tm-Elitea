---
id: ELITEA-1381
title: "ADO31 - Delete Wiki Page by ID"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [toolkit, wiki, sdk, ado]
requirements: []
---
# ELITEA-1381: ADO31 - Delete Wiki Page by ID

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'delete_page_by_id' tool deletes a wiki page using its ID

## Preconditions

ADO Wiki toolkit is configured with valid credentials.
Target wiki page exists with a known page ID.
Test user has write permissions on the wiki.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Wiki toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `delete_page_by_id` tool with the wiki identifier and the numeric page ID | Tool executes without error |
| 3 | Verify the response confirms the page was deleted (e.g., HTTP 204, 'deleted', or empty success response) | Deletion confirmation is present |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
page_deleted = true
no_error = true
