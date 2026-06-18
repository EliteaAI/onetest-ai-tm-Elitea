---
id: ELITEA-1113
title: "SharePoint – Multiple File Formats (.png, .pdf, .txt) Accepted by \"Upload file\""
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:image-generation, feat:toolkits]
requirements: [3180]
---
# ELITEA-1113: SharePoint – Multiple File Formats (.png, .pdf, .txt) Accepted by "Upload file"

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the SharePoint 'Upload file' tool accepts multiple file formats when uploading from an Artifact bucket.

## Preconditions

- ELITEA platform accessible
- SharePoint toolkit configured with 'Upload file' tool enabled
- Artifact bucket contains test files: test-file.png, test-file.pdf, test-file.txt
- A valid SharePoint site and document library are available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Upload file' with the SharePoint target and filepath /my-bucket/test-file.png | Tool executes successfully; .png file appears in the SharePoint document library |
| 2 | Invoke 'Upload file' with the same SharePoint target and filepath /my-bucket/test-file.pdf | Tool executes successfully; .pdf file appears in the SharePoint document library |
| 3 | Invoke 'Upload file' with the same SharePoint target and filepath /my-bucket/test-file.txt | Tool executes successfully; .txt file appears in the SharePoint document library |

## Expected Final State

Tool executes successfully; .txt file appears in the SharePoint document library

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
