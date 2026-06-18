---
id: ELITEA-0435
title: "Chat + Upload → TestRail: User-Uploaded File Uploaded to TC Steps"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:testrail, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0435: Chat + Upload → TestRail: User-Uploaded File Uploaded to TC Steps

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file uploaded by the user via the Chat paperclip is saved to an Artifact bucket and can be uploaded to the Steps field of a TestRail test case.

## Preconditions

- ELITEA Chat is accessible
- Artifact Toolkit is configured with a writable bucket
- TestRail toolkit is configured with valid credentials and has 'Add file to case' tool enabled
- A valid TestRail test case ID is available
- A local file (e.g., steps-screenshot.png) is available for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Ensure Artifact Toolkit and TestRail toolkit are connected | Both toolkits are active in the current Chat session |
| 2 | Use the paperclip button to upload a local file (e.g., steps-screenshot.png) and send a prompt: 'Save this file to /my-bucket/steps-screenshot.png' | File is saved to the Artifact bucket; Chat confirms the path |
| 3 | Send a follow-up prompt: 'Upload /my-bucket/steps-screenshot.png to the Steps field of TestRail test case [case_id]' | Chat invokes the upload tool targeting the Steps field and reports success |
| 4 | Navigate to TestRail and open the test case | steps-screenshot.png appears in the Steps field |

## Expected Final State

steps-screenshot.png appears in the Steps field

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
