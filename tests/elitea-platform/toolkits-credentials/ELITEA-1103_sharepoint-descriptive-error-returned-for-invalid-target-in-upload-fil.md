---
id: ELITEA-1103
title: "SharePoint – Descriptive Error Returned for Invalid Target in \"Upload file\""
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:image-generation, feat:toolkits]
requirements: [3180]
---
# ELITEA-1103: SharePoint – Descriptive Error Returned for Invalid Target in "Upload file"

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a descriptive error message is returned when an invalid SharePoint target (site or document library) is provided to the SharePoint 'Upload file' tool.

## Preconditions

- ELITEA platform accessible
- SharePoint toolkit configured with 'Upload file' tool enabled
- Artifact bucket contains a valid file at /my-bucket/test-file.png

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke 'Upload file' with a non-existent SharePoint site or document library and a valid filepath /my-bucket/test-file.png | Tool returns a descriptive error message indicating the SharePoint target was not found; no crash or silent failure |

## Expected Final State

Tool returns a descriptive error message indicating the SharePoint target was not found; no crash or silent failure

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
