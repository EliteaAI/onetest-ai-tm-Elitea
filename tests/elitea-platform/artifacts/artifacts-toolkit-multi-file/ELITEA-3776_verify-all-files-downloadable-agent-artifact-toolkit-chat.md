---
id: ELITEA-3776
title: "Verify all files are downloadable when agent with Artifact Toolkit creates multiple files via Chat"
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
- An agent with Artifact toolkit attached exists
- The agent is added as a participant in a Chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Agent prompt | "Create and save 3 files: summary.txt, details.txt, and appendix.txt, each with distinct content" |
| Expected file count | 3 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat` and open or create a conversation with the agent as participant | Chat page loads with agent participant visible |
| 2 | Send the prompt: "Create and save 3 files: summary.txt, details.txt, and appendix.txt, each with distinct content" | Agent processes and responds confirming all 3 files were saved |
| 3 | Navigate to `{{base_url}}/app/artifacts` and open the configured bucket | Bucket file list is displayed |
| 4 | Verify the file list contains all 3 files: summary.txt, details.txt, appendix.txt | All 3 files appear in the list |
| 5 | Download each of the 3 files one by one | Each file downloads with the correct distinct content |

## Expected Final State

All 3 files created by the agent via Chat are present in the artifact bucket and each is individually downloadable with correct content.

## Pass/Fail Criteria

**Pass:**
- All 3 files are visible in the artifact bucket
- Each file downloads successfully with correct content

**Fail:**
- Fewer than 3 files appear in the artifact bucket
- Any file cannot be downloaded or has incorrect/empty content
