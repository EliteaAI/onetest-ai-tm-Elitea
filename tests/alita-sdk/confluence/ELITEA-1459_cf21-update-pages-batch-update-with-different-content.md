---
id: ELITEA-1459
title: "CF21 - Update Pages (Batch Update with Different Content)"
priority: critical
type: functional
module: confluence
status: ready
execution_type: automated
tags: [update_pages, confluence, batch, pages, smoke]
requirements: []
---
# ELITEA-1459: CF21 - Update Pages (Batch Update with Different Content)

**Module:** Confluence · **Priority:** Critical · **Type:** Functional

**Objective:** Verify update_pages tool updates multiple pages with different content in a batch operation, where each page receives its own corresponding content from the new_contents list.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID env var is set
Multiple existing page IDs available with write permissions
new_contents list contains different content per page

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
Page IDs: [CF_PAGE_ID_1, CF_PAGE_ID_2] (existing pages with write permissions)
new_contents: ['Content for page 1 - CF21 {timestamp}', 'Content for page 2 - CF21 {timestamp}'] (different content per page)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call update_pages tool with multiple page IDs and new_contents list with different content per page (e.g., 2 page IDs with 2 different content strings) | All pages updated with their corresponding content, response contains status list |
| 2 | LLM validates: response is a list with update status for each page, each page received its specific content, no errors during batch update | Validation confirms update_pages correctly applies different content to each page in batch |

## Expected Final State

Validation confirms update_pages correctly applies different content to each page in batch

## Pass/Fail Criteria

PASS: Each page updated with its corresponding content, response list contains status for each page
FAIL: Tool crashes, wrong content applied to pages, response missing per-page status
