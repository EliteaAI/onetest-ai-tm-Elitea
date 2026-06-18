---
id: ELITEA-1213
title: "SharePoint Index Data — include_extensions Restricts Indexing to Specified File Types Only"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, eng:frontend, feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4897]
---
# ELITEA-1213: SharePoint Index Data — include_extensions Restricts Indexing to Specified File Types Only

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when `include_extensions` is set to a specific type, only files of that type are indexed and all other types are excluded.

**Coverage:**
- `include_extensions` includes only matching files
- Files of other types are not indexed
- Multiple matching files are all included

## Preconditions

- Logged in to {{base_url}} with Toolkit access
- SharePoint library contains: `report.csv`, `ignored.csv`, `notes.docx`
- Index Data and Search Index tools enabled

## Test Data

- Include Extensions: `["*.csv"]`
- Skip Extensions: empty
- Search filter 1: `{"Name": "report.csv"}`
- Search filter 2: `{"Name": "ignored.csv"}`
- Search filter 3: `{"Name": "notes.docx"}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open + Create New Index; set Include Extensions to ["*.csv"]; leave Skip Extensions empty | Fields populated correctly |
| 2 | Run index and wait for completion | Indexing completes without errors |
| 3 | Search with filter {"Name": "report.csv"} | File found in results |
| 4 | Search with filter {"Name": "ignored.csv"} | File found in results |
| 5 | Search with filter {"Name": "notes.docx"} | No results returned — .docx excluded by include filter |

## Expected Final State

No results returned — .docx excluded by include filter

## Pass/Fail Criteria

**Pass:**
- Both `report.csv` and `ignored.csv` are found in search results
- `notes.docx` is not found in search results

**Fail:**
- Either CSV file is missing from results
- `notes.docx` appears in results
