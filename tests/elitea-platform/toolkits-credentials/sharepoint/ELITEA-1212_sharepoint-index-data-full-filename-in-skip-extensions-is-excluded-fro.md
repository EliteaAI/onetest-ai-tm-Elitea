---
id: ELITEA-1212
title: "SharePoint Index Data — Full Filename in skip_extensions Is Excluded from Indexing"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, eng:frontend, feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4897]
---
# ELITEA-1212: SharePoint Index Data — Full Filename in skip_extensions Is Excluded from Indexing

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a file whose full name (e.g., `testdataEJ.csv`) is listed in `skip_extensions` is not indexed, even when `include_extensions` would otherwise include it.

**Coverage:**
- Full filename entry in `skip_extensions` with `*.csv` in `include_extensions`
- Indexed collection does not contain the skipped file
- Non-skipped CSV files are still indexed

## Preconditions

- Logged in to {{base_url}} as a user with Toolkit creation rights
- SharePoint toolkit configured with valid credentials
- SharePoint document library contains: `testdataEJ.csv`, `report.csv`
- Index Data and Search Index tools enabled on the toolkit
- PgVector and Embedding Model configured in Settings → AI Configuration

## Test Data

- Include Extensions: `["*.csv"]`
- Skip Extensions: `["testdataEJ.csv"]`
- Search filter 1: `{"Name": "testdataEJ.csv"}`
- Search filter 2: `{"Name": "report.csv"}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → select SharePoint toolkit → open Indexes tab → click + Create New Index | Index creation form opens |
| 2 | Set Include Extensions to ["*.csv"] | Field populated with ["*.csv"] |
| 3 | Set Skip Extensions to ["testdataEJ.csv"] | Field populated with ["testdataEJ.csv"] |
| 4 | Click Run / Start Indexing and wait for completion | Indexing completes with no errors; no "Dependent documents for 'testdataEJ.csv' were processed" message appears in output |
| 5 | Use Search Index tool with filter {"Name": "testdataEJ.csv"} | No results returned — file was not indexed |
| 6 | Use Search Index tool with filter {"Name": "report.csv"} | File is found in results — non-skipped CSV was indexed |

## Expected Final State

File is found in results — non-skipped CSV was indexed

## Pass/Fail Criteria

**Pass:**
- `testdataEJ.csv` returns no search results
- `report.csv` is present in search results
- No error messages during indexing

**Fail:**
- `testdataEJ.csv` appears in any search result
- "Dependent documents for 'testdataEJ.csv' were processed" message appears in output
