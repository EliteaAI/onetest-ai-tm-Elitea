---
id: ELITEA-0443
title: "Chat + Image Gen → Jira: AI-Generated Image Uploaded to Issue Comment"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0443: Chat + Image Gen → Jira: AI-Generated Image Uploaded to Issue Comment

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an AI-generated image produced in Chat (using gpt-5.2 with Image Creation toggle ON) is saved to an Artifact bucket and can be uploaded to a Comment on a Jira issue.

## Preconditions

- ELITEA Chat is accessible
- gpt-5.2 model is available
- Image Creation toggle is available in Chat settings
- Artifact Toolkit is configured with a writable bucket
- Jira toolkit is configured with valid credentials and has the upload tool enabled
- A valid Jira issue key is available (e.g., PROJ-123)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Select gpt-5.2 model and enable the Image Creation toggle | Image Creation toggle is ON; gpt-5.2 is selected |
| 2 | Ensure Artifact Toolkit and Jira toolkit are connected to the Chat | Both toolkits are active in the current Chat session |
| 3 | Send a prompt: 'Generate a workflow diagram and save it to /my-bucket/workflow.png' | Image is generated and saved to the Artifact bucket; Chat confirms the file path |
| 4 | Send a follow-up prompt: 'Upload /my-bucket/workflow.png as a comment on Jira issue [issue_key]' | Chat invokes the upload tool targeting the Jira issue Comment and reports success |
| 5 | Navigate to Jira and open the issue, check the Comments section | workflow.png appears in a comment on the Jira issue |

## Expected Final State

workflow.png appears in a comment on the Jira issue

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
