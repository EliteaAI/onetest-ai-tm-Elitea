---
id: ELITEA-1114
title: "Jira – Multiple File Formats (.png, .pdf, .txt) Accepted by \"Add file to issue description\""
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, feat:toolkits]
requirements: [3180]
---
# ELITEA-1114: Jira – Multiple File Formats (.png, .pdf, .txt) Accepted by "Add file to issue description"

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Jira 'Add file to issue description' tool accepts multiple file formats when uploading from an Artifact bucket.

## Preconditions

- ELITEA platform accessible
- Jira toolkit configured with 'Add file to issue description' tool enabled
- Artifact bucket contains test files: test-file.png, test-file.pdf, test-file.txt
- A valid Jira issue key is available (e.g., PROJ-123)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to issue description' with issue_key and filepath /my-bucket/test-file.png | Tool executes successfully; .png file reference appears in the Jira issue description |
| 2 | Invoke 'Add file to issue description' with the same issue_key and filepath /my-bucket/test-file.pdf | Tool executes successfully; .pdf file reference appears in the Jira issue description |
| 3 | Invoke 'Add file to issue description' with the same issue_key and filepath /my-bucket/test-file.txt | Tool executes successfully; .txt file reference appears in the Jira issue description |

## Expected Final State

Tool executes successfully; .txt file reference appears in the Jira issue description

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
