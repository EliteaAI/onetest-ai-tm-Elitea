---
id: ELITEA-3779
title: "Re-validate createFile subfolder path preservation for single file via Chat with Artifact Toolkit"
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
- Agent with Artifact toolkit is available as Chat participant (same setup as ELITEA-0321)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Agent prompt | "Save a file named report.txt with content 'Subfolder test' to the path output/reports/" |
| Expected path | `output/reports/report.txt` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chat with the agent as participant | Chat loads with agent visible |
| 2 | Send: "Save a file named report.txt with content 'Subfolder test' to the path output/reports/" | Agent confirms the file was saved at the specified path |
| 3 | Navigate to `{{base_url}}/app/artifacts`, open the bucket, navigate to `output/reports/` | Subfolder structure is present |
| 4 | Verify report.txt is present at `output/reports/report.txt` | File is visible at the correct path |
| 5 | Download report.txt | File downloads with content "Subfolder test" |

## Expected Final State

The file is stored at the correct subfolder path and is downloadable with correct content. The fix for multi-file creation has not broken subfolder path handling.

## Pass/Fail Criteria

**Pass:**
- File appears at the correct subfolder path
- File downloads with correct content

**Fail:**
- File is missing or stored at the wrong path
- File content is empty or incorrect
