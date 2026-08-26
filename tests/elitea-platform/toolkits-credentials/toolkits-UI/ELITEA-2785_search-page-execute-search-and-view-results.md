---
id: ELITEA-2785
title: "Search Page - Execute Search and View Results"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, smoke, search, execution]
requirements: []
---
# ELITEA-2785: Search Page - Execute Search and View Results

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional / Smoke

**Objective:** Verify search execution and results display in the Results panel.

**Coverage:**
- Required parameter validation blocks empty submission
- Search executes successfully with valid parameters
- Loading indicator displays during execution
- Results panel shows formatted output
- Results are scrollable for long content

## Preconditions

- Logged in to {{base_url}}
- A toolkit with a completed index containing searchable content

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexed content |
| Index | Completed index with documents |
| Query | "test case" |
| Cut Off | 0.1 |
| Search Top | 10 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an index's Search page and select "Search Index" tool. | Tool parameters displayed. |
| 2 | Leave the Query field empty and click "Search" button. | Validation error appears: "Please fill out this field." or similar browser validation. |
| 3 | Enter "test case" in the Query field. | Query value accepted. |
| 4 | Adjust Cut Off slider to 0.1. | Slider and value update to 0.1. |
| 5 | Set Search Top to 10. | Value set to 10. |
| 6 | Click the "Search" button. | Loading indicator appears; button may show loading state. |
| 7 | Wait for search to complete. | Loading indicator disappears; Results panel updates. |
| 8 | Observe the Results panel. | Search results displayed with formatted output (document matches, relevance scores, content snippets). |
| 9 | If results are long, verify scrolling works. | Results panel has vertical scrollbar; content is scrollable. |

## Expected Final State

Results panel displays formatted search results matching the query, with all content accessible via scrolling.

## Pass/Fail Criteria

**Pass:**
- Validation prevents empty required fields
- Search executes successfully
- Loading indicator displays during execution
- Results show relevant matches
- Long results are scrollable

**Fail:**
- No validation on required fields
- Search fails or hangs
- No loading indicator
- Results empty when content exists
- Results truncated without scroll
