---
id: ELITEA-1474
title: "CF02 - Get Pages with Label"
priority: high
type: functional
module: confluence
status: ready
execution_type: automated
tags: [get_pages_with_label, confluence, labels, pages]
requirements: []
---
# ELITEA-1474: CF02 - Get Pages with Label

**Module:** Confluence · **Priority:** High · **Type:** Functional

**Objective:** Verify get_pages_with_label tool retrieves pages tagged with a specific label, returning page IDs, titles, and content.

## Preconditions

Confluence toolkit is configured and authenticated
CF_TOOLKIT_ID and CF_SPACE_KEY env vars are set
At least one page with the target label exists in Confluence

## Test Data

CF_TOOLKIT_ID: Confluence toolkit ID
CF_SPACE_KEY: Confluence space key
CF_LABEL: Label name used to filter pages (at least one page must have this label)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_pages_with_label tool with target label name (CF_LABEL) | Pages returned without errors for the specified label |
| 2 | LLM validates: returned pages have the target label, each result includes page ID and title, only matching pages included | Validation confirms get_pages_with_label correctly retrieves pages with the specified label |

## Expected Final State

Validation confirms get_pages_with_label correctly retrieves pages with the specified label

## Pass/Fail Criteria

PASS: Pages returned matching the label, each with page ID
FAIL: Empty result when pages with label exist, non-matching pages included
