---
id: ELITEA-1458
title: "CF22 - Update Pages (Batch Update with Same Content)"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [same-content, update_pages, confluence, batch, pages]
requirements: []
---
# ELITEA-1458: CF22 - Update Pages (Batch Update with Same Content)

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify update_pages tool updates multiple pages with the same (identical) content in a batch operation, handling the bulk update scenario where all pages receive the same content.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID env var is set
Multiple existing page IDs available with write permissions
new_contents contains single shared content value

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
Page IDs: [CF_PAGE_ID_1, CF_PAGE_ID_2] (existing pages with write permissions)
new_contents: ['Shared content for all pages - CF22 {timestamp}'] (single content applied to all pages)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call update_pages tool with multiple page IDs and new_contents list containing a single shared content value (e.g., 2 page IDs with 1 content string applied to all) | All pages updated with the same content, response contains status list |
| 2 | LLM validates: response is a list with update status for all pages, all pages received the same content, bulk-same-content scenario handled correctly | Validation confirms update_pages correctly handles bulk update with identical content for all pages |

## Expected Final State

Validation confirms update_pages correctly handles bulk update with identical content for all pages

## Pass/Fail Criteria

PASS: All pages updated with the same content, response list contains status for each page
FAIL: Tool crashes, pages not all updated, status list incomplete
