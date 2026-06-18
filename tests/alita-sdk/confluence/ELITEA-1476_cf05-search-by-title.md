---
id: ELITEA-1476
title: "CF05 - Search by Title"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [search_by_title, confluence, search]
requirements: []
---
# ELITEA-1476: CF05 - Search by Title

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify search_by_title tool searches for pages by query text in page title only (not content), returning matching pages.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID and CF_SPACE_KEY env vars are set
At least one page with a title matching the search query exists

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_SPACE_KEY: Confluence space key
CF_TITLE_SEARCH_QUERY: Query text known to appear in at least one page title

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call search_by_title tool with a query text known to match at least one page title | Search results returned containing pages with matching titles |
| 2 | LLM validates: returned pages have titles matching the query, only title-match pages included, each result has page ID and title | Validation confirms search_by_title correctly searches titles only and returns matching pages |

## Expected Final State

Validation confirms search_by_title correctly searches titles only and returns matching pages

## Pass/Fail Criteria

PASS: Pages returned whose titles match the query, results limited to title matches only
FAIL: Content-only matches included, empty results when title matches exist
