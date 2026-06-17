---
id: ELITEA-0438
title: "Chat + Image Gen → SharePoint: AI-Generated Image Uploaded to SharePoint"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:image-generation, image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0438: Chat + Image Gen → SharePoint: AI-Generated Image Uploaded to SharePoint

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an AI-generated image produced in Chat (using gpt-5.2 with Image Creation toggle ON) is saved to an Artifact bucket and can be uploaded to SharePoint.

## Preconditions

- ELITEA Chat is accessible
- gpt-5.2 model is available
- Image Creation toggle is available in Chat settings
- Artifact Toolkit is configured with a writable bucket
- SharePoint toolkit is configured with valid credentials and has 'Upload file' tool enabled
- A valid SharePoint site and document library are available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Select gpt-5.2 model and enable the Image Creation toggle | Image Creation toggle is ON; gpt-5.2 is selected |
| 2 | Ensure Artifact Toolkit and SharePoint toolkit are connected to the Chat | Both toolkits are active in the current Chat session |
| 3 | Send a prompt: 'Generate a project plan diagram and save it to /my-bucket/project-plan.png' | Image is generated and saved to the Artifact bucket; Chat confirms the file path |
| 4 | Send a follow-up prompt: 'Upload /my-bucket/project-plan.png to the SharePoint document library' | Chat invokes 'Upload file' tool and reports success |
| 5 | Navigate to the SharePoint document library | project-plan.png appears in the SharePoint document library |

## Expected Final State

project-plan.png appears in the SharePoint document library

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
