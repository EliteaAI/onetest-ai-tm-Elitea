---
id: ELITEA-1384
title: "ADO28 - Modify Wiki Page"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [toolkit, wiki, sdk, ado]
requirements: []
---
# ELITEA-1384: ADO28 - Modify Wiki Page

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the ADO 'modify_wiki_page' tool creates or updates wiki page content

## Preconditions

ADO Wiki toolkit is configured with valid credentials.
Target wiki exists and the test user has write permissions.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Wiki toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `modify_wiki_page` tool with the wiki identifier, page path (e.g., '/AI-Test-Page'), and new content | Tool executes without error |
| 3 | Verify the response confirms the page was created or updated (e.g., page ID, version, or 'success') | Success confirmation is present in the response |
| 4 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
page_saved = true
no_error = true
