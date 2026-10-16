---
id: ELITEA-3780
title: "Re-validate single-file createFile via Pipeline toolkit node is unaffected after fix"
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
- A pipeline with Artifact toolkit node configured for single-file output exists (same setup as ELITEA-0322)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Expected output | 1 file: pipeline-single.txt |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/pipelines` and open the single-file pipeline | Pipeline loads |
| 2 | Execute the pipeline | Pipeline runs and completes without error |
| 3 | Navigate to `{{base_url}}/app/artifacts` and open the configured bucket | Bucket file list displays |
| 4 | Verify pipeline-single.txt is present | File appears in the list |
| 5 | Download pipeline-single.txt | File downloads with correct content |

## Expected Final State

Single-file pipeline creation remains functional after the multi-file fix.

## Pass/Fail Criteria

**Pass:**
- Exactly 1 expected file appears in the bucket
- File downloads with correct content

**Fail:**
- File is absent from the bucket after pipeline execution
- File downloads with empty or incorrect content
