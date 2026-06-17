---
id: ELITEA-0437
title: "Chat + Upload → TestRail: User-Uploaded File Uploaded to TC Attachment"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:testrail, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0437: Chat + Upload → TestRail: User-Uploaded File Uploaded to TC Attachment

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file uploaded by the user via the Chat paperclip is saved to an Artifact bucket and can be uploaded to a TestRail test case as a TC attachment.

## Preconditions

- ELITEA Chat is accessible
- Artifact Toolkit is configured with a writable bucket
- TestRail toolkit is configured with valid credentials and has 'Add file to case' tool enabled
- A valid TestRail test case ID is available
- A local file (e.g., screenshot.png) is available for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Ensure Artifact Toolkit and TestRail toolkit are connected | Both toolkits are active in the current Chat session |
| 2 | Use the paperclip (file upload) button to upload a local file (e.g., screenshot.png) and send a prompt: 'Save this file to the artifact bucket as /my-bucket/screenshot.png' | File is saved to the Artifact bucket at the specified path; Chat confirms |
| 3 | Send a follow-up prompt: 'Upload /my-bucket/screenshot.png to TestRail test case [case_id] as an attachment' | Chat invokes 'Add file to case' tool and reports success |
| 4 | Navigate to TestRail and open the test case | screenshot.png appears in the TC attachment section |

## Expected Final State

screenshot.png appears in the TC attachment section

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
