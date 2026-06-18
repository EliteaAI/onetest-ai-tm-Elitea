---
id: ELITEA-1460
title: "CF20 - Update Page by Title (Page Not Found)"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [update_page_by_title, error-handling, confluence, negative, pages]
requirements: []
---
# ELITEA-1460: CF20 - Update Page by Title (Page Not Found)

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify update_page_by_title tool handles non-existent page title gracefully, returning error message starting with "Page with title" and "not found" without crashing.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID and CF_SPACE_KEY env vars are set
NEGATIVE test — title used must not exist in Confluence space

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_SPACE_KEY: Confluence space key
Non-existent page title: 'NONEXISTENT PAGE TITLE CF20 XYZ 99999' (must not exist in Confluence)
Expected error format: starts with 'Page with title' and contains 'not found'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call update_page_by_title tool with a page title that does not exist in the Confluence space (e.g., 'NONEXISTENT PAGE TITLE CF20 XYZ 99999') | Tool executes without crashing, returns error message |
| 2 | LLM validates: response starts with 'Page with title' and contains 'not found', error is informative, no unhandled exceptions | Validation confirms update_page_by_title handles non-existent page title gracefully with correct error message |

## Expected Final State

Validation confirms update_page_by_title handles non-existent page title gracefully with correct error message

## Pass/Fail Criteria

PASS: Error message starts with "Page with title" and contains "not found", no crash
FAIL: Tool throws exception, returns wrong error format, or unexpectedly succeeds
