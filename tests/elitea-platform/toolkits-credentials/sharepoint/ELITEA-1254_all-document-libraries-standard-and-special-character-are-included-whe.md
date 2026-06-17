---
id: ELITEA-1254
title: "All Document Libraries (Standard and Special-Character) Are Included When No Path Is Specified"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1254: All Document Libraries (Standard and Special-Character) Are Included When No Path Is Specified

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that `index_data` without a path indexes content from all document libraries on the site — both standard-named (`hyphen-folder`) and special-character-named (`sharepoint-index#1`) — in a single operation.

**Coverage:**
- No-path indexing covers both standard-named and special-character-named libraries
- Content unique to `hyphen-folder` is searchable after indexing
- Content unique to `sharepoint-index#1` is searchable after indexing
- Index collection visible via List Collections

## Preconditions

- Logged in to {{base_url}} as a user with Owner or Editor role in a Private project
- SharePoint toolkit configured per Pre-Testing Setup
- `hyphen-folder` contains a .txt file with unique phrase: "standard folder content phrase"
- `sharepoint-index#1` contains a .txt file with unique phrase: "special char folder content phrase"
- PgVector and Embedding Model configured; Index Data tool enabled

## Test Data

- Index Name: `alllibs`
- Path: (empty)
- Unique phrase in hyphen-folder/data.txt: "standard folder content phrase"
- Unique phrase in sharepoint-index#1/data.txt: "special char folder content phrase"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → SharePoint toolkit → Indexes tab | Indexes tab is displayed |
| 2 | Click + (New Index); enter `alllibs` as Index Name; leave Path empty; click Index | Indexing job starts |
| 3 | Wait for the job to complete | Job completes without error; `alllibs` appears in the index list |
| 4 | In the Run tab for `alllibs`, use Search Index with the phrase "standard folder content phrase" | At least one result is returned, citing a file from `hyphen-folder` |
| 5 | Use Search Index with the phrase "special char folder content phrase" | At least one result is returned, citing a file from `sharepoint-index#1` |

## Expected Final State

At least one result is returned, citing a file from `sharepoint-index#1`

## Pass/Fail Criteria

**Pass:**
- Both `hyphen-folder` and `sharepoint-index#1` content is returned in separate searches
- Total indexed count reflects files from all libraries

**Fail:**
- Search for `hyphen-folder` phrase returns no results
- Search for `sharepoint-index#1` phrase returns no results (library skipped due to special characters)
