---
id: ELITEA-0427
title: "Chat + Upload → SharePoint: User-Uploaded File Uploaded to SharePoint"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0427: Chat + Upload → SharePoint: User-Uploaded File Uploaded to SharePoint

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file uploaded by the user via the Chat paperclip is saved to an Artifact bucket and can be uploaded to SharePoint.

## Preconditions

- ELITEA Chat is accessible
- Artifact Toolkit is configured with a writable bucket
- SharePoint toolkit is configured with valid credentials and has 'Upload file' tool enabled
- A valid SharePoint site and document library are available
- A local file (e.g., document.pdf) is available for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Ensure Artifact Toolkit and SharePoint toolkit are connected | Both toolkits are active in the current Chat session |
| 2 | Use the paperclip button to upload a local file (e.g., document.pdf) and send a prompt: 'Save this file to /my-bucket/document.pdf' | File is saved to the Artifact bucket; Chat confirms the path |
| 3 | Send a follow-up prompt: 'Upload /my-bucket/document.pdf to the SharePoint document library' | Chat invokes 'Upload file' tool and reports success |
| 4 | Navigate to the SharePoint document library | document.pdf appears in the SharePoint document library |

## Expected Final State

document.pdf appears in the SharePoint document library

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
