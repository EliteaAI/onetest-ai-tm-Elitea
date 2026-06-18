---
id: ELITEA-1407
title: "ADO05 - Get Wiki Page with Image Processing"
priority: medium
type: functional
module: ado
status: ready
execution_type: automated
tags: [toolkit, wiki, sdk, ado]
requirements: []
---
# ELITEA-1407: ADO05 - Get Wiki Page with Image Processing

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify 'get_wiki_page' retrieves wiki content with processed image descriptions using custom prompt

## Preconditions

ADO Wiki toolkit is configured with valid credentials.
ADO_WIKI_TOOLKIT_ID and ADO_WIKI_TOOLKIT_NAME are set.
A wiki page with embedded images exists in the ADO project wiki.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure ADO Wiki toolkit with valid credentials | Toolkit initialized successfully |
| 2 | Call `get_wiki_page` tool with the wiki identifier and page path | Tool executes and returns wiki page content |
| 3 | Verify the page content is retrieved and non-empty | Content string has length > 0 |
| 4 | Verify images in the page content have been processed into text descriptions using the custom prompt | Image references are replaced by descriptive text rather than raw image syntax |
| 5 | Validate no error message is present in the result | Result does not contain 'error' or 'failed' |

## Expected Final State

Result does not contain 'error' or 'failed'

## Pass/Fail Criteria

test_passed = true
tool_executed = true
content is non-empty
image descriptions are processed (not raw image syntax)
