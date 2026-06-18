---
id: ELITEA-1258
title: "index_data Without Path Correctly Indexes Excel (.xlsx) Files From Special-Character Libraries"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1258: index_data Without Path Correctly Indexes Excel (.xlsx) Files From Special-Character Libraries

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that `AlitaExcelLoader` processes `.xlsx` files without error when `index_data` is invoked without a path on a site containing special-character document library names — directly validating the specific crash traced to `AlitaExcelLoader.load()`.

**Coverage:**
- `index_data` runs without a `path` on a site with special-character library names containing `.xlsx` files
- `AlitaExcelLoader` processes the `.xlsx` file without raising `AttributeError: 'str' object has no attribute 'items'`
- Index completes successfully
- Indexed `.xlsx` content is queryable via Search Index

## Preconditions

- Logged in to {{base_url}} as a user with Owner or Editor role in a Private project
- SharePoint toolkit configured with valid Azure AD Client ID and Client Secret pointing to the test SharePoint site
- SharePoint site contains document libraries: `doc-lib_for/sharepoint^retest()-/@!$-test~@#%^&*:;,.`, `sharepoint-index#1`, `hyphen-folder` — each with at least data.txt and file.xlsx
- PgVector and Embedding Model configured in Settings → AI Configuration
- Index Data tool is enabled in the toolkit configuration
- At least one `.xlsx` file (e.g., file.xlsx) exists in each of the special-character libraries with known searchable cell content

## Test Data

- Index Name: `xlsxtest`
- Path field: (empty)
- Search query after indexing: content phrase known to exist in file.xlsx (e.g., a cell value from the spreadsheet)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select the SharePoint toolkit → open the Indexes tab | Indexes tab is displayed |
| 2 | Click + (New Index) | New Index form appears |
| 3 | Enter `xlsxtest` in Index Name; leave Path empty | Fields populated as specified |
| 4 | Click Index | Indexing job starts |
| 5 | Wait for the indexing job to complete | Job completes without error; no "Index processing error" banner |
| 6 | Select the `xlsxtest` index → open the Run sub-tab | Run panel opens with Search Index tool available |
| 7 | Select Search Index, enter a query matching known content from file.xlsx (e.g., a cell value from the file) | Query is submitted |
| 8 | Observe the search results | At least one result is returned; the result citation references file.xlsx from one of the special-character libraries |

## Expected Final State

At least one result is returned; the result citation references file.xlsx from one of the special-character libraries

## Pass/Fail Criteria

**Pass:**
- Indexing completes without `AttributeError` or crash
- file.xlsx content is returned as a search result with correct source citation

**Fail:**
- `AttributeError: 'str' object has no attribute 'items'` is raised during indexing
- "Tool execution failed" message appears
- No results are returned for `.xlsx` content after successful indexing
