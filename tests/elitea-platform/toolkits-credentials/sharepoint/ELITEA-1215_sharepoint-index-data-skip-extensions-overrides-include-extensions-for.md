---
id: ELITEA-1215
title: "SharePoint Index Data — skip_extensions Overrides include_extensions for Conflicting File"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, eng:frontend, feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4897]
---
# ELITEA-1215: SharePoint Index Data — skip_extensions Overrides include_extensions for Conflicting File

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a file matching both `include_extensions` and `skip_extensions` is excluded — `skip_extensions` must always take priority.

**Coverage:**
- Conflict resolution: skip wins over include for the same file
- Non-conflicting file included by `include_extensions` is indexed normally

## Preconditions

- Logged in to {{base_url}} with Toolkit access
- SharePoint library contains: `ignored.csv`, `report.csv`
- Index Data and Search Index tools enabled

## Test Data

- Include Extensions: `["*.csv"]`
- Skip Extensions: `["ignored.csv"]`
- Search filter 1: `{"Name": "ignored.csv"}`
- Search filter 2: `{"Name": "report.csv"}`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open + Create New Index; set Include Extensions to ["*.csv"]; set Skip Extensions to ["ignored.csv"] | Both fields populated correctly |
| 2 | Run index and wait for completion | Indexing completes without errors |
| 3 | Search with filter {"Name": "ignored.csv"} | No results returned — skip rule took priority over include rule |
| 4 | Search with filter {"Name": "report.csv"} | File found in results — unaffected by skip rule |

## Expected Final State

File found in results — unaffected by skip rule

## Pass/Fail Criteria

**Pass:**
- `ignored.csv` returns no results
- `report.csv` is present in results

**Fail:**
- `ignored.csv` appears in any result
- `report.csv` is unexpectedly excluded
