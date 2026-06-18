---
id: ELITEA-1463
title: "CF11 - Site Search (Happy Path)"
priority: critical
type: functional
module: confluence
status: ready
execution_type: automated
tags: [site_search, confluence, search, smoke]
requirements: []
---
# ELITEA-1463: CF11 - Site Search (Happy Path)

**Module:** Confluence · **Priority:** Critical · **Type:** Functional

**Objective:** Verify site_search tool performs site-wide search and returns page data with preview text. Tool should return one or more page entries with page_id, page_title, page_url, and preview fields formatted with '---' separators.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID env var is set
At least one page matching the search query exists in Confluence

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_SEARCH_QUERY: Search query known to match at least one page in Confluence
Expected response format: entries with page_id, page_title, page_url, preview separated by '---'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call site_search tool with a search query known to match existing pages in Confluence | Search results returned without errors |
| 2 | LLM validates: response contains one or more page entries, each entry has page_id, page_title, page_url, and preview fields, entries are separated by '---' delimiter | Validation confirms site_search returns properly structured page results with preview data |

## Expected Final State

Validation confirms site_search returns properly structured page results with preview data

## Pass/Fail Criteria

PASS: Returns one or more entries with page_id, page_title, page_url, and preview fields, formatted with '---' separators
FAIL: Empty result, missing required fields, unformatted output
