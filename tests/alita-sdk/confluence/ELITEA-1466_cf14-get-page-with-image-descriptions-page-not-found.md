---
id: ELITEA-1466
title: "CF14 - Get Page with Image Descriptions (Page Not Found)"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [get_page_with_image_descriptions, error-handling, confluence, negative, pages]
requirements: []
---
# ELITEA-1466: CF14 - Get Page with Image Descriptions (Page Not Found)

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify get_page_with_image_descriptions tool handles non-existent page ID gracefully, returning a message starting with "Page with ID" and "not found" without crashing.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID env var is set
NEGATIVE test — invalid page ID used that does not exist in Confluence

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
Invalid page ID: '999999999999' (must not exist in Confluence)
Expected message format: starts with 'Page with ID' and contains 'not found'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_page_with_image_descriptions tool with an invalid/non-existent page ID (e.g., '999999999999') | Tool executes without crashing, returns error message |
| 2 | LLM validates: response starts with 'Page with ID' and contains 'not found', error is informative, no unhandled exceptions | Validation confirms get_page_with_image_descriptions handles invalid page ID gracefully with correct error message format |

## Expected Final State

Validation confirms get_page_with_image_descriptions handles invalid page ID gracefully with correct error message format

## Pass/Fail Criteria

PASS: Returns message starting with "Page with ID" and containing "not found", no crash
FAIL: Tool throws unhandled exception, returns empty response, or confusing error
