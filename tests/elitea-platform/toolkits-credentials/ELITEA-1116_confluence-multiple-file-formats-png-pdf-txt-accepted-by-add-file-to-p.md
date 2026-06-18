---
id: ELITEA-1116
title: "Confluence – Multiple File Formats (.png, .pdf, .txt) Accepted by \"Add file to page\""
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, feat:toolkits]
requirements: [3180]
---
# ELITEA-1116: Confluence – Multiple File Formats (.png, .pdf, .txt) Accepted by "Add file to page"

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Confluence 'Add file to page' tool accepts multiple file formats when uploading from an Artifact bucket.

## Preconditions

- ELITEA platform accessible
- Confluence toolkit configured with 'Add file to page' tool enabled
- Artifact bucket contains test files: test-file.png, test-file.pdf, test-file.txt
- A valid Confluence page ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Add file to page' with page_id and filepath /my-bucket/test-file.png | Tool executes successfully; .png file appears on the Confluence page |
| 2 | Invoke 'Add file to page' with the same page_id and filepath /my-bucket/test-file.pdf | Tool executes successfully; .pdf file appears on the Confluence page |
| 3 | Invoke 'Add file to page' with the same page_id and filepath /my-bucket/test-file.txt | Tool executes successfully; .txt file appears on the Confluence page |

## Expected Final State

Tool executes successfully; .txt file appears on the Confluence page

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
