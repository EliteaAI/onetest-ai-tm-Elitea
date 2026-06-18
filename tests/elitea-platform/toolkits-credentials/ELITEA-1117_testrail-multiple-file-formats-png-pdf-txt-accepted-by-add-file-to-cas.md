---
id: ELITEA-1117
title: "TestRail – Multiple File Formats (.png, .pdf, .txt) Accepted by \"Add file to case\""
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:image-generation, integration:testrail, feat:toolkits]
requirements: [3180]
---
# ELITEA-1117: TestRail – Multiple File Formats (.png, .pdf, .txt) Accepted by "Add file to case"

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the TestRail 'Add file to case' tool accepts multiple file formats when uploading from an Artifact bucket.

## Preconditions

- ELITEA platform accessible
- TestRail toolkit configured with 'Add file to case' tool enabled
- Artifact bucket contains test files: test-file.png, test-file.pdf, test-file.txt
- A valid TestRail test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to case' with case_id and filepath /my-bucket/test-file.png | Tool executes successfully; .png file appears as attachment in TestRail |
| 2 | Invoke 'Add file to case' with the same case_id and filepath /my-bucket/test-file.pdf | Tool executes successfully; .pdf file appears as attachment in TestRail |
| 3 | Invoke 'Add file to case' with the same case_id and filepath /my-bucket/test-file.txt | Tool executes successfully; .txt file appears as attachment in TestRail |

## Expected Final State

Tool executes successfully; .txt file appears as attachment in TestRail

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
