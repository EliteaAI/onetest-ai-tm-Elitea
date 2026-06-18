---
id: ELITEA-1383
title: "ADO29 - Rename Wiki Page"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [toolkit, wiki, sdk, ado]
requirements: []
---
# ELITEA-1383: ADO29 - Rename Wiki Page

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'rename_wiki_page' tool renames a wiki page

## Preconditions

ADO Wiki toolkit is configured with valid credentials.
Target wiki page exists at the specified path.
Test user has write permissions on the wiki.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Wiki toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `rename_wiki_page` tool with the wiki identifier, current page path, and new page name | Tool executes without error |
| 3 | Verify the response confirms the page was renamed (e.g., new page path or 'success') | Rename confirmation is present in the response |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
page_renamed = true
no_error = true
