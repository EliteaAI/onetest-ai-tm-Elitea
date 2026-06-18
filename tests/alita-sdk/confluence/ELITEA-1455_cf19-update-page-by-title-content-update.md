---
id: ELITEA-1455
title: "CF19 - Update Page by Title (Content Update)"
priority: critical
type: functional
module: confluence
status: ready
execution_type: automated
tags: [update_page_by_title, confluence, pages, smoke]
requirements: []
---
# ELITEA-1455: CF19 - Update Page by Title (Content Update)

**Module:** Confluence · **Priority:** Critical · **Type:** Functional

**Objective:** Verify update_page_by_title tool updates page content by locating the page via its title, returning success message or updated page details.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID and CF_SPACE_KEY env vars are set
Page with target title exists and is writable (CF_UPDATE_PAGE_TITLE)

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_SPACE_KEY: Confluence space key
CF_UPDATE_PAGE_TITLE: Exact title of existing page to update
New content: 'Updated content via title - CF19 {timestamp}'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call update_page_by_title tool with CF_UPDATE_PAGE_TITLE (known existing page title) and new content to replace | Page located by title and content updated, success response returned |
| 2 | LLM validates: page was found by title and updated, response contains success message or updated page details, no errors | Validation confirms update_page_by_title correctly locates page by title and updates its content |

## Expected Final State

Validation confirms update_page_by_title correctly locates page by title and updates its content

## Pass/Fail Criteria

PASS: Page located by title and content updated, response confirms success
FAIL: Tool crashes, wrong page updated, update not reflected, page not found
