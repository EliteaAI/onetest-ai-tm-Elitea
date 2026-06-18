---
id: ELITEA-1118
title: "SharePoint Toolkit – \"Upload file\" Tool Present, Toggleable, and Executes Successfully"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:image-generation, feat:toolkits]
requirements: [3180]
---
# ELITEA-1118: SharePoint Toolkit – "Upload file" Tool Present, Toggleable, and Executes Successfully

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the "Upload file" tool is visible in the SharePoint toolkit panel, can be enabled/disabled, and successfully uploads a file to SharePoint using an Artifact bucket path.

## Preconditions

- ELITEA platform accessible at {{base_url}}
- User is logged in with valid credentials
- SharePoint toolkit is configured with valid credentials
- An Artifact Toolkit bucket exists with at least one file (e.g., /my-bucket/test-file.png)
- A valid SharePoint site and document library are available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA → Toolkits → SharePoint toolkit configuration page | SharePoint toolkit settings panel is displayed |
| 2 | Scroll through the available tools list and locate 'Upload file' | 'Upload file' tool is visible in the tools list |
| 3 | Toggle the 'Upload file' tool OFF, save, then toggle it ON and save again | Tool toggles without error; enabled state persists after save |
| 4 | Invoke the 'Upload file' tool with a valid SharePoint target and filepath (e.g., /my-bucket/test-file.png) | Tool executes without error and returns a success response |
| 5 | Navigate to the SharePoint document library used in step 4 | The file (test-file.png) appears in the SharePoint document library |

## Expected Final State

The file (test-file.png) appears in the SharePoint document library

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
