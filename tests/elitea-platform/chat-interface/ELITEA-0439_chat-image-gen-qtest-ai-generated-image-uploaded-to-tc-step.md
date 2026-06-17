---
id: ELITEA-0439
title: "Chat + Image Gen → QTest: AI-Generated Image Uploaded to TC Step"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:qtest, image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0439: Chat + Image Gen → QTest: AI-Generated Image Uploaded to TC Step

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an AI-generated image produced in Chat (using gpt-5.2 with Image Creation toggle ON) is saved to an Artifact bucket and can be uploaded to a step within a QTest test case.

## Preconditions

- ELITEA Chat is accessible
- gpt-5.2 model is available
- Image Creation toggle is available in Chat settings
- Artifact Toolkit is configured with a writable bucket
- QTest toolkit is configured with valid credentials and has 'Add file to test case' tool enabled
- A valid QTest test case ID with at least one step is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Select gpt-5.2 model and enable the Image Creation toggle | Image Creation toggle is ON; gpt-5.2 is selected |
| 2 | Ensure Artifact Toolkit and QTest toolkit are connected to the Chat | Both toolkits are active in the current Chat session |
| 3 | Send a prompt: 'Generate a step illustration diagram and save it to /my-bucket/step-illustration.png' | Image is generated and saved to the Artifact bucket; Chat confirms the file path |
| 4 | Send a follow-up prompt: 'Upload /my-bucket/step-illustration.png to a step in QTest test case [test_case_id]' | Chat invokes the upload tool targeting the TC step and reports success |
| 5 | Navigate to QTest and open the test case, inspect the steps | step-illustration.png appears within a step of the QTest test case |

## Expected Final State

step-illustration.png appears within a step of the QTest test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
