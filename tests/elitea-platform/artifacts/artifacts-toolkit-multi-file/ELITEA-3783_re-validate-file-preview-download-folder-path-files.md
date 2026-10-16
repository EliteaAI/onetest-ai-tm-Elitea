---
id: ELITEA-3783
title: "Re-validate file preview and download for files stored in folder paths remain functional"
priority: high
type: regression
module: artifacts
status: draft
execution_type: manual
tags: [r-2.0.4, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#5313]
---

## Preconditions

- User is logged in to `{{base_url}}`
- An agent with Artifact toolkit is used to create a file at a non-root folder path (same scenario as ELITEA-0311)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/artifacts` |
| File path | `subfolder/regression-check.txt` |
| File content | "Preview and download regression check" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Use agent to create a file at `subfolder/regression-check.txt` | Agent confirms file created at the path |
| 2 | Navigate to `{{base_url}}/app/artifacts`, open the bucket, navigate to `subfolder/` | File `regression-check.txt` is visible |
| 3 | Click the preview action for regression-check.txt | File content renders correctly in the preview panel |
| 4 | Click the download action for regression-check.txt | File downloads with filename `regression-check.txt` and correct content |

## Expected Final State

Files stored in folder paths via the Artifact toolkit are still previewable and downloadable after the multi-file fix.

## Pass/Fail Criteria

**Pass:**
- File is found at the expected subfolder path
- Preview renders the correct content
- Download produces a file with the correct name and content

**Fail:**
- File is not visible at the subfolder path
- Preview fails to render or shows empty content
- Download fails or produces a file with wrong name/content
