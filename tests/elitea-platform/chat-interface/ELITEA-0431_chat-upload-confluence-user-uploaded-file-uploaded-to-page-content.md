---
id: ELITEA-0431
title: "Chat + Upload → Confluence: User-Uploaded File Uploaded to Page Content"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0431: Chat + Upload → Confluence: User-Uploaded File Uploaded to Page Content

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file uploaded by the user via the Chat paperclip is saved to an Artifact bucket and can be uploaded to the page content of a Confluence page.

## Preconditions

- ELITEA Chat is accessible
- Artifact Toolkit is configured with a writable bucket
- Confluence toolkit is configured with valid credentials and has 'Add file to page' tool enabled
- A valid Confluence page ID is available
- A local file (e.g., architecture.png) is available for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Ensure Artifact Toolkit and Confluence toolkit are connected | Both toolkits are active in the current Chat session |
| 2 | Use the paperclip button to upload a local file (e.g., architecture.png) and send a prompt: 'Save this file to /my-bucket/architecture.png' | File is saved to the Artifact bucket; Chat confirms the path |
| 3 | Send a follow-up prompt: 'Upload /my-bucket/architecture.png to the content of Confluence page [page_id]' | Chat invokes 'Add file to page' tool targeting page content and reports success |
| 4 | Navigate to Confluence and open the page | architecture.png appears in the page content |

## Expected Final State

architecture.png appears in the page content

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
