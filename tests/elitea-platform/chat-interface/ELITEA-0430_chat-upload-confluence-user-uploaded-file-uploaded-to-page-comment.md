---
id: ELITEA-0430
title: "Chat + Upload → Confluence: User-Uploaded File Uploaded to Page Comment"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [integration:confluence, feat:image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0430: Chat + Upload → Confluence: User-Uploaded File Uploaded to Page Comment

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file uploaded by the user via the Chat paperclip is saved to an Artifact bucket and can be uploaded to a Comment on a Confluence page.

## Preconditions

- ELITEA Chat is accessible
- Artifact Toolkit is configured with a writable bucket
- Confluence toolkit is configured with valid credentials and has the upload tool enabled
- A valid Confluence page ID is available
- A local file (e.g., review-notes.png) is available for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Ensure Artifact Toolkit and Confluence toolkit are connected | Both toolkits are active in the current Chat session |
| 2 | Use the paperclip button to upload a local file (e.g., review-notes.png) and send a prompt: 'Save this file to /my-bucket/review-notes.png' | File is saved to the Artifact bucket; Chat confirms the path |
| 3 | Send a follow-up prompt: 'Upload /my-bucket/review-notes.png as a comment on Confluence page [page_id]' | Chat invokes the upload tool targeting the page Comment and reports success |
| 4 | Navigate to Confluence and open the page, check the Comments section | review-notes.png appears in a comment on the Confluence page |

## Expected Final State

review-notes.png appears in a comment on the Confluence page

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
