---
id: ELITEA-1372
title: "ADO40 - Link Work Items to Wiki Page"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [work-items, toolkit, wiki, sdk, ado]
requirements: []
---
# ELITEA-1372: ADO40 - Link Work Items to Wiki Page

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'link_work_items_to_wiki_page' tool links work items to a wiki page

## Preconditions

ADO Work Items toolkit is configured with valid credentials.
Work items with known IDs exist in the project.
Target wiki page exists at the specified path.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Work Items toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `link_work_items_to_wiki_page` tool with a list of work_item_ids and the wiki page path | Tool executes without error |
| 3 | Verify the response confirms links were created between the work items and the wiki page | Response contains success confirmation for the linking operation |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
links_created = true
no_error = true
