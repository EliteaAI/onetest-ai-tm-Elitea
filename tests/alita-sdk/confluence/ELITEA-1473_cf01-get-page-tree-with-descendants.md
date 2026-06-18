---
id: ELITEA-1473
title: "CF01 - Get Page Tree with Descendants"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [get_page_tree, confluence, pages, smoke]
requirements: []
---
# ELITEA-1473: CF01 - Get Page Tree with Descendants

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify get_page_tree tool retrieves complete hierarchical structure including all descendant pages from a parent page.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID and CF_SPACE_KEY env vars are set
Parent page with descendant pages exists (CF_PAGE_ID)

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_SPACE_KEY: Confluence space key
CF_PAGE_ID: ID of parent page with descendant pages

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_page_tree tool with the target parent page ID (CF_PAGE_ID) | Page tree returned without errors containing hierarchical structure |
| 2 | LLM validates: response includes parent page and all descendant pages, page IDs and titles are present, structure is hierarchical | Validation confirms get_page_tree retrieves complete hierarchical structure with descendants |

## Expected Final State

Validation confirms get_page_tree retrieves complete hierarchical structure with descendants

## Pass/Fail Criteria

PASS: Page tree returned containing parent page and descendant pages in hierarchical structure, page IDs and titles present
FAIL: Empty result, missing descendant pages, or malformed structure
