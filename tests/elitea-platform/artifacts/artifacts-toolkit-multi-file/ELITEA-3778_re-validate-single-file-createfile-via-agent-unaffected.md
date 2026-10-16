---
id: ELITEA-3778
title: "Re-validate single-file createFile via agent is unaffected after multi-file fix"
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
- An agent with Artifact toolkit attached exists (same setup as ELITEA-0320)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Agent prompt | "Create and save exactly 1 file named single-output.txt with content 'Regression check'" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/agents` and open the agent with Artifact toolkit | Agent detail page loads |
| 2 | In the embedded chat, send: "Create and save exactly 1 file named single-output.txt with content 'Regression check'" | Agent confirms the file was saved |
| 3 | Navigate to `{{base_url}}/app/artifacts` and open the configured bucket | Bucket file list is displayed |
| 4 | Verify single-output.txt appears in the list | single-output.txt is present |
| 5 | Download single-output.txt | File downloads with content "Regression check" |

## Expected Final State

The single file created by the agent is present in the artifact bucket and downloadable. No duplicate or missing files.

## Pass/Fail Criteria

**Pass:**
- Exactly 1 file (single-output.txt) appears in the bucket
- File downloads with correct content

**Fail:**
- File is absent from the bucket
- File downloads with empty or incorrect content
