---
id: ELITEA-0444
title: "Chat + Image Gen → Jira: AI-Generated Image Uploaded to Issue Description"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, image-generation, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0444: Chat + Image Gen → Jira: AI-Generated Image Uploaded to Issue Description

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an AI-generated image produced in Chat (using gpt-5.2 with Image Creation toggle ON) is saved to an Artifact bucket and can be uploaded to the Description field of a Jira issue.

## Preconditions

- ELITEA Chat is accessible
- gpt-5.2 model is available
- Image Creation toggle is available in Chat settings
- Artifact Toolkit is configured with a writable bucket
- Jira toolkit is configured with valid credentials and has 'Add file to issue description' tool enabled
- A valid Jira issue key is available (e.g., PROJ-123)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Select gpt-5.2 model and enable the Image Creation toggle | Image Creation toggle is ON; gpt-5.2 is selected |
| 2 | Ensure Artifact Toolkit and Jira toolkit are connected to the Chat | Both toolkits are active in the current Chat session |
| 3 | Send a prompt: 'Generate a bug screenshot mockup and save it to /my-bucket/bug-screenshot.png' | Image is generated and saved to the Artifact bucket; Chat confirms the file path |
| 4 | Send a follow-up prompt: 'Upload /my-bucket/bug-screenshot.png to the Description field of Jira issue [issue_key]' | Chat invokes 'Add file to issue description' tool and reports success |
| 5 | Navigate to Jira and open the issue | bug-screenshot.png appears in the Description field of the Jira issue |

## Expected Final State

bug-screenshot.png appears in the Description field of the Jira issue

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
