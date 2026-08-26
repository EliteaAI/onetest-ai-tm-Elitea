---
id: ELITEA-2795
title: "Search Results Copy and Scroll Functionality"
priority: medium
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, search, results]
requirements: []
---
# ELITEA-2795: Search Results Copy and Scroll Functionality

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify search results can be copied and long results are scrollable.

**Coverage:**
- Results panel displays formatted output
- Long results are scrollable
- Copy action available and functional
- Results content is selectable

## Preconditions

- Logged in to {{base_url}}
- An index with sufficient indexed content to produce multiple search results

## Test Data

| Field | Value |
|-------|-------|
| Index | Index with substantial content |
| Query | A term that returns multiple results |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an index's Search page. | Search page displays. |
| 2 | Select "Search Index" tool and enter a query that returns multiple results. | Query entered. |
| 3 | Click "Search" button. | Search executes and returns results. |
| 4 | Observe the Results panel content. | Results displayed with document matches, scores, snippets. |
| 5 | If results are long, verify scrollbar appears. | Vertical scrollbar visible in Results panel. |
| 6 | Scroll through the results. | All results are accessible via scrolling. |
| 7 | Look for copy icon/button on the results. | Copy action button visible (if available). |
| 8 | Click the copy button or use Ctrl+C to select and copy text. | Results content copied to clipboard. |
| 9 | Paste the copied content into a text editor. | Copied content matches the results. |

## Expected Final State

Results are fully viewable via scrolling and can be copied for use elsewhere.

## Pass/Fail Criteria

**Pass:**
- Long results have scrollbar
- All results accessible via scrolling
- Copy functionality works (button or text selection)
- Copied content is accurate

**Fail:**
- Results truncated without scroll
- Cannot scroll to all results
- Copy functionality missing or broken
- Copied content corrupted
