---
id: ELITEA-0442
title: "Chat + Image Gen → Confluence: AI-Generated Image Uploaded to Page Content"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0442: Chat + Image Gen → Confluence: AI-Generated Image Uploaded to Page Content

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an AI-generated image produced in Chat (using gpt-5.2 with Image Creation toggle ON) is saved to an Artifact bucket and can be uploaded to the page content of a Confluence page.

## Preconditions

- ELITEA Chat is accessible
- gpt-5.2 model is available
- Image Creation toggle is available in Chat settings
- Artifact Toolkit is configured with a writable bucket
- Confluence toolkit is configured with valid credentials and has 'Add file to page' tool enabled
- A valid Confluence page ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Select gpt-5.2 model and enable the Image Creation toggle | Image Creation toggle is ON; gpt-5.2 is selected |
| 2 | Ensure Artifact Toolkit and Confluence toolkit are connected to the Chat | Both toolkits are active in the current Chat session |
| 3 | Send a prompt: 'Generate an architecture diagram and save it to /my-bucket/architecture.png' | Image is generated and saved to the Artifact bucket; Chat confirms the file path |
| 4 | Send a follow-up prompt: 'Upload /my-bucket/architecture.png to the content of Confluence page [page_id]' | Chat invokes 'Add file to page' tool targeting page content and reports success |
| 5 | Navigate to Confluence and open the page | architecture.png appears in the page content |

## Expected Final State

architecture.png appears in the page content

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
