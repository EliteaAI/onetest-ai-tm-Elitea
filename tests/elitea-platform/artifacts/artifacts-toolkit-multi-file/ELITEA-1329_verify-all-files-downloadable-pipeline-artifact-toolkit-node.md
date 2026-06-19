---
id: ELITEA-1329
title: "Verify all files are downloadable when Pipeline with Artifact Toolkit node creates multiple files"
priority: critical
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [r-2.0.4, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#5313]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A pipeline exists with an Artifact toolkit node configured to produce multiple output files
- The Artifact toolkit node is connected to a valid bucket

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline node instruction | Produces 3 files: pipeline-out-1.txt, pipeline-out-2.txt, pipeline-out-3.txt |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/pipelines` and open the pipeline with the Artifact toolkit node | Pipeline detail page loads |
| 2 | Execute the pipeline | Pipeline runs and completes without error |
| 3 | Navigate to `{{base_url}}/app/artifacts` and open the configured bucket | Bucket file list is displayed |
| 4 | Verify all 3 expected files are listed: pipeline-out-1.txt, pipeline-out-2.txt, pipeline-out-3.txt | All 3 files appear in the file list |
| 5 | Download each file | Each file downloads with correct content |

## Expected Final State

All files produced by the pipeline's Artifact toolkit node are present in the artifact bucket and downloadable.

## Pass/Fail Criteria

**Pass:**
- All 3 pipeline-generated files appear in the artifact bucket
- Each file downloads successfully with correct content

**Fail:**
- Only 1 (or fewer than 3) files appear in the bucket after pipeline execution
- Any file fails to download
