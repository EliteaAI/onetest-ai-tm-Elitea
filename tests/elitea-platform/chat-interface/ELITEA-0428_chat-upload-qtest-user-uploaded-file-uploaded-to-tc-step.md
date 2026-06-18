---
id: ELITEA-0428
title: "Chat + Upload → QTest: User-Uploaded File Uploaded to TC Step"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:qtest, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0428: Chat + Upload → QTest: User-Uploaded File Uploaded to TC Step

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file uploaded by the user via the Chat paperclip is saved to an Artifact bucket and can be uploaded to a step within a QTest test case.

## Preconditions

- ELITEA Chat is accessible
- Artifact Toolkit is configured with a writable bucket
- QTest toolkit is configured with valid credentials and has 'Add file to test case' tool enabled
- A valid QTest test case ID with at least one step is available
- A local file (e.g., step-illustration.png) is available for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Ensure Artifact Toolkit and QTest toolkit are connected | Both toolkits are active in the current Chat session |
| 2 | Use the paperclip button to upload a local file (e.g., step-illustration.png) and send a prompt: 'Save this file to /my-bucket/step-illustration.png' | File is saved to the Artifact bucket; Chat confirms the path |
| 3 | Send a follow-up prompt: 'Upload /my-bucket/step-illustration.png to a step in QTest test case [test_case_id]' | Chat invokes the upload tool targeting the TC step and reports success |
| 4 | Navigate to QTest and open the test case, inspect the steps | step-illustration.png appears within a step of the QTest test case |

## Expected Final State

step-illustration.png appears within a step of the QTest test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
