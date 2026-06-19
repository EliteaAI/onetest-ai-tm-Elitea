---
id: ELITEA-1336
title: "Re-validate Artifact Toolkit Test Settings createFile single-file execution after fix"
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
- An Artifact toolkit exists and is accessible via Toolkits (same setup as ELITEA-1128)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/toolkits` |
| Tool | createFile |
| File name | `test-settings-check.txt` |
| File content | "Test settings regression check" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/toolkits`, open the Artifact toolkit | Toolkit detail page loads with Test Settings panel |
| 2 | In the Test Settings panel, select the `createFile` tool | createFile parameters are shown |
| 3 | Enter file name: `test-settings-check.txt` and content: `"Test settings regression check"` | Parameters are populated |
| 4 | Click the Run Tool button | Execution completes successfully; result panel shows success |
| 5 | Navigate to `{{base_url}}/app/artifacts` and open the configured bucket | Bucket file list displayed |
| 6 | Verify `test-settings-check.txt` is present and download it | File is present and downloads with correct content |

## Expected Final State

The Artifact toolkit Test Settings createFile tool executes successfully and the created file is visible and downloadable in the artifact bucket.

## Pass/Fail Criteria

**Pass:**
- Test Settings execution returns a success result
- File appears in the artifact bucket
- File downloads with correct content

**Fail:**
- Test Settings execution returns an error
- File does not appear in the artifact bucket
- File downloads with empty or incorrect content
