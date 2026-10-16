---
id: ELITEA-3781
title: "Verify subfolder paths are preserved for all files when agent creates multiple files at different paths"
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
- An agent with Artifact toolkit attached exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Agent prompt | "Create 3 files at different paths: docs/file1.txt, reports/file2.csv, and output/file3.json — each with distinct content" |
| Expected paths | `docs/file1.txt`, `reports/file2.csv`, `output/file3.json` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/agents` and open the agent with Artifact toolkit | Agent detail page loads |
| 2 | In the embedded chat, send the multi-path file creation prompt | Agent confirms 3 files were saved at the specified paths |
| 3 | Navigate to `{{base_url}}/app/artifacts`, open the bucket, navigate to `docs/` | file1.txt is present in `docs/` |
| 4 | Navigate to `reports/` in the same bucket | file2.csv is present in `reports/` |
| 5 | Navigate to `output/` in the same bucket | file3.json is present in `output/` |
| 6 | Download each of the 3 files | Each file downloads with its distinct correct content |

## Expected Final State

All 3 files are stored at their respective subfolder paths and each is downloadable with correct content. No file is placed at the wrong path or at the bucket root.

## Pass/Fail Criteria

**Pass:**
- Each file is found at its expected subfolder path
- All files download with correct distinct content

**Fail:**
- Any file is missing, placed at the wrong path, or stored at the bucket root instead
- Any file downloads with empty or incorrect content
