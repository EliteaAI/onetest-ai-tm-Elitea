---
id: ELITEA-1471
title: "CF08 - List Pages with Label"
priority: medium
type: functional
module: confluence
status: ready
execution_type: automated
tags: [list_pages_with_label, confluence, labels, pages]
requirements: []
---
# ELITEA-1471: CF08 - List Pages with Label

**Module:** Confluence · **Priority:** Medium · **Type:** Functional

**Objective:** Verify list_pages_with_label tool retrieves a list of page IDs and titles for pages tagged with a specific label, distinct from the full content retrieval of get_pages_with_label.

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
| 1 | Call list_pages_with_label tool with target label name (CF_LABEL) | List of pages returned without errors for the specified label |
| 2 | LLM validates: response is a list of pages with specified label, each entry has page ID and title, list is properly structured | Validation confirms list_pages_with_label returns correctly structured list of page identifiers for the label |

## Expected Final State

Validation confirms list_pages_with_label returns correctly structured list of page identifiers for the label

## Pass/Fail Criteria

PASS: List of page IDs and titles returned for the label, properly structured
FAIL: Empty list when labeled pages exist, missing page metadata
