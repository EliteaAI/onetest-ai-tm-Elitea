---
id: ELITEA-1243
title: "Search indexed OneNote content via index search tools"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1243: Search indexed OneNote content via index search tools

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that Search index, Stepback search index, and Stepback summary index correctly return results from indexed OneNote content, including multi-page matches and empty-query handling.

**Coverage:**
- Search index returns exact keyword matches from indexed OneNote pages
- Multi-page matches all returned
- Stepback search index returns contextually related pages
- Stepback summary index produces a summary from indexed content
- Non-existent keyword returns empty result cleanly

## Preconditions

- OneNote content indexed via Index data with "Include Onenote" checked
- At least 2 OneNote pages with distinct content already indexed

## Test Data

- Exact keyword in one page: [keyword1]
- Broader topic keyword across multiple pages: [keyword2]
- Non-existent keyword: [nonexistent-xyz]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `Search index` with [keyword1]. | Indexed OneNote page(s) containing the keyword returned. |
| 2 | Invoke `Search index` with [keyword2] (present in multiple pages). | All matching pages returned — not limited to one result. |
| 3 | Invoke `Stepback search index` with a broader conceptual query related to [keyword2]. | Contextually related OneNote pages returned, including pages without the exact query word. |
| 4 | Invoke `Stepback summary index` with a topic query. | A summary response derived from indexed OneNote content returned. |
| 5 | Invoke `Search index` with [nonexistent-xyz]. | Empty result returned — no error. |

## Expected Final State

Empty result returned — no error.

## Pass/Fail Criteria

**Pass:**
- All search tools return relevant results; multi-page matches returned; empty query returns cleanly

**Fail:**
- Search returns no results when matching content exists; any tool errors
