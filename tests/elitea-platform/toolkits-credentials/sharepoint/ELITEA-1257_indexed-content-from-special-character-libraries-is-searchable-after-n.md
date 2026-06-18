---
id: ELITEA-1257
title: "Indexed Content From Special-Character Libraries Is Searchable After No-Path Indexing"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1257: Indexed Content From Special-Character Libraries Is Searchable After No-Path Indexing

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that after a successful `index_data` run without a path, the indexed content from special-character libraries can be retrieved using the Search Index tool.

**Coverage:**
- Search Index returns results after a no-path indexing run
- Citations reference source documents from special-character library names
- Natural language query returns content from data.txt stored in `sharepoint-index#1`

## Preconditions

- A successful no-path index named `nopath` exists (TC: index_data Without Path Succeeds on Site With Special-Character Document Library Names must have passed)
- data.txt in `sharepoint-index#1` contains a unique, searchable phrase (e.g., "SharePoint retest content unique phrase")

## Test Data

- Index to search: `nopath`
- Search query: a phrase unique to data.txt content (e.g., "SharePoint retest content unique phrase")
- Expected source document: data.txt from `sharepoint-index#1`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select the SharePoint toolkit → open the Indexes tab | Indexes tab is displayed with `nopath` visible in the list |
| 2 | Click on the `nopath` index entry | The index detail panel opens |
| 3 | Click the Run sub-tab | Run panel opens with search tool options |
| 4 | Select Search Index | Search input field is displayed |
| 5 | Enter the unique phrase from data.txt in `sharepoint-index#1` | Query is typed in the search field |
| 6 | Submit the search query | Query is sent |
| 7 | Observe the returned results | At least one result is returned |
| 8 | Verify the result citation references the correct source document and library | Result citation shows data.txt from the `sharepoint-index#1` library |

## Expected Final State

Result citation shows data.txt from the `sharepoint-index#1` library

## Pass/Fail Criteria

**Pass:**
- Search returns at least one result for the unique phrase
- Result citation correctly references data.txt from the special-character library

**Fail:**
- No results returned for a known-content phrase
- Results are returned but citations reference wrong documents or no library name
