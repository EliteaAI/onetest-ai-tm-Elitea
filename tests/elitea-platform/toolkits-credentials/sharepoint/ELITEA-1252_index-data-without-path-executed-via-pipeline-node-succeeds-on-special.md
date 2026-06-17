---
id: ELITEA-1252
title: "index_data Without Path Executed via Pipeline Node Succeeds on Special-Character Libraries"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1252: index_data Without Path Executed via Pipeline Node Succeeds on Special-Character Libraries

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a Pipeline node configured with the SharePoint toolkit's Index Data tool and no path runs successfully end-to-end when the SharePoint site contains special-character library names.

**Coverage:**
- Pipeline Toolkit node with `index_data` configured (no path)
- Pipeline run completes without "Tool execution failed" or `AttributeError`
- New index with non-zero count created in the toolkit's Indexes tab after pipeline run

## Preconditions

- A Pipeline exists in the Private project with a SharePoint Toolkit node that has Index Data configured with no path and index name suffix `pipe`
- Special-character libraries exist on the SharePoint site per Pre-Testing Setup
- PgVector and Embedding Model configured; Index Data tool enabled in the toolkit

## Test Data

- Pipeline: SharePoint Toolkit node → index_data, Index Name: `pipe`, Path: (empty)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines; open the pipeline with the SharePoint index_data node | Pipeline configuration view opens |
| 2 | Run the pipeline | Pipeline execution starts |
| 3 | Monitor the SharePoint Toolkit node execution | Node completes without "Tool execution failed" or error traceback |
| 4 | Wait for the pipeline run to finish | Overall pipeline run status shows success |
| 5 | Navigate to Toolkits → SharePoint toolkit → Indexes tab | Indexes tab displayed |
| 6 | Locate the `pipe` index in the list | `pipe` index is present |
| 7 | Verify the total indexed count | Count is ≥ 1 (files from the SharePoint site were processed) |

## Expected Final State

Count is ≥ 1 (files from the SharePoint site were processed)

## Pass/Fail Criteria

**Pass:**
- Pipeline node completes without error
- `pipe` index created with non-zero total indexed count

**Fail:**
- Toolkit node shows "Tool execution failed"
- `AttributeError` appears in pipeline node output
- No index or count 0 after pipeline run
