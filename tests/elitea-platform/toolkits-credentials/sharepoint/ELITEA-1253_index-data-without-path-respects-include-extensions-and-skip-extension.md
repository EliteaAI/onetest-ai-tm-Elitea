---
id: ELITEA-1253
title: "index_data Without Path Respects include_extensions and skip_extensions Filters Across All Libraries Including Special-Character Libraries"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1253: index_data Without Path Respects include_extensions and skip_extensions Filters Across All Libraries Including Special-Character Libraries

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that `include_extensions` and `skip_extensions` filters are correctly applied to all document libraries — including special-character-named ones — when `index_data` is run without a path.

**Coverage:**
- `include_extensions = ["*.txt"]` with no path: only `.txt` content indexed; `.xlsx` excluded — verified for both standard and special-character libraries
- `skip_extensions = ["*.xlsx"]` with no path: `.xlsx` files excluded; `.txt` included — verified for both library types
- Filter behavior consistent regardless of library name containing special characters

## Preconditions

- Logged in to {{base_url}} as a user with Owner or Editor role in a Private project
- SharePoint toolkit configured per Pre-Testing Setup
- Each library contains both data.txt and file.xlsx with distinct searchable content
- PgVector and Embedding Model configured; Index Data tool enabled

## Test Data

Run 1: Index Name `incext`, include_extensions: ["*.txt"], Path: empty — Expected: .txt indexed, .xlsx NOT indexed
Run 2: Index Name `skipext`, skip_extensions: ["*.xlsx"], Path: empty — Expected: .txt indexed, .xlsx NOT indexed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → SharePoint toolkit → Indexes tab → New Index | New Index form opens |
| 2 | Enter `incext` as Index Name; set include_extensions to ["*.txt"]; leave Path empty; click Index | Indexing starts |
| 3 | Wait for completion | Job completes without error |
| 4 | In Run tab for `incext`, use Search Index with a phrase unique to data.txt | Result returned citing a .txt source |
| 5 | In Run tab for `incext`, use Search Index with a phrase unique to file.xlsx | No result returned (.xlsx was not indexed) |
| 6 | Create another New Index named `skipext`; set skip_extensions to ["*.xlsx"]; leave Path empty; click Index | Job starts |
| 7 | Wait for completion | Job completes without error |
| 8 | In Run tab for `skipext`, use Search Index with a phrase unique to file.xlsx | No result returned (.xlsx skipped) |
| 9 | In Run tab for `skipext`, use Search Index with a phrase unique to data.txt | Result returned citing a .txt source |

## Expected Final State

Result returned citing a .txt source

## Pass/Fail Criteria

**Pass:**
- `include_extensions` correctly limits indexing to .txt only (no .xlsx results)
- `skip_extensions` correctly excludes .xlsx (no .xlsx results, .txt results present)
- Filters apply consistently to special-character-named libraries

**Fail:**
- .xlsx content appears in search results when excluded by filter
- .txt content is missing from results when included by filter
- Filter behavior differs between standard and special-character libraries
