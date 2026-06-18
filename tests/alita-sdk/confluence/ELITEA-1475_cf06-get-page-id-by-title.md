---
id: ELITEA-1475
title: "CF06 - Get Page ID by Title"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [get_page_id_by_title, confluence, pages]
requirements: []
---
# ELITEA-1475: CF06 - Get Page ID by Title

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify get_page_id_by_title tool retrieves the page ID when provided with a page title, returning the numeric page identifier.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID and CF_SPACE_KEY env vars are set
Known page with exact title exists in Confluence space

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_SPACE_KEY: Confluence space key
CF_PAGE_TITLE: Exact title of known existing page
Expected CF_PAGE_ID: Known page ID corresponding to that title

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_page_id_by_title tool with the exact title of a known existing page | Page ID returned as numeric identifier |
| 2 | LLM validates: returned ID is a valid numeric page identifier, matches the known page ID for that title | Validation confirms get_page_id_by_title returns correct page ID for the given title |

## Expected Final State

Validation confirms get_page_id_by_title returns correct page ID for the given title

## Pass/Fail Criteria

PASS: Numeric page ID returned matching known value for the page title
FAIL: Wrong page ID returned, empty result, non-numeric ID
