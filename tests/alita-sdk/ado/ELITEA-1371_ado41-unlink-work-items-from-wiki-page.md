---
id: ELITEA-1371
title: "ADO41 - Unlink Work Items from Wiki Page"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, wiki, sdk, ado]
requirements: []
---
# ELITEA-1371: ADO41 - Unlink Work Items from Wiki Page

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'unlink_work_items_from_wiki_page' tool removes work item links from a wiki page

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
Work items are already linked to the target wiki page (e.g., by ADO40 running first).
Test user has write permissions.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Ensure prerequisite: Work items are linked to the wiki page (ADO40 has run) | Work item links exist on the wiki page |
| 2 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 3 | Call `unlink_work_items_from_wiki_page` tool with the list of work_item_ids and the wiki page path | Tool executes without error |
| 4 | Verify the response confirms links were removed from the wiki page | Response contains success confirmation for the unlinking operation |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
links_removed = true
no_error = true
