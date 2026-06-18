---
id: ELITEA-0445
title: "Chat + Image Gen → TestRail: AI-Generated Image Uploaded to TC Expected Result"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:testrail, image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0445: Chat + Image Gen → TestRail: AI-Generated Image Uploaded to TC Expected Result

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an AI-generated image produced in Chat (using gpt-5.2 with Image Creation toggle ON) is saved to an Artifact bucket and can be uploaded to the Expected Result field of a TestRail test case.

## Preconditions

- ELITEA Chat is accessible
- gpt-5.2 model is available
- Image Creation toggle is available in Chat settings
- Artifact Toolkit is configured with a writable bucket
- TestRail toolkit is configured with valid credentials and has 'Add file to case' tool enabled
- A valid TestRail test case ID is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Select gpt-5.2 model and enable the Image Creation toggle | Image Creation toggle is ON; gpt-5.2 is selected |
| 2 | Ensure Artifact Toolkit and TestRail toolkit are connected to the Chat | Both toolkits are active in the current Chat session |
| 3 | Send a prompt: 'Generate a screenshot mockup of the expected UI state and save it to /my-bucket/expected-result.png' | Image is generated and saved to the Artifact bucket; Chat confirms the file path |
| 4 | Send a follow-up prompt: 'Upload /my-bucket/expected-result.png to the Expected Result field of TestRail test case [case_id]' | Chat invokes the upload tool targeting the Expected Result field and reports success |
| 5 | Navigate to TestRail and open the test case | expected-result.png appears in the Expected Result field of the test case |

## Expected Final State

expected-result.png appears in the Expected Result field of the test case

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
