---
id: ELITEA-0433
title: "Chat + Upload → Jira: User-Uploaded File Uploaded to Issue Description"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0433: Chat + Upload → Jira: User-Uploaded File Uploaded to Issue Description

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file uploaded by the user via the Chat paperclip is saved to an Artifact bucket and can be uploaded to the Description field of a Jira issue.

## Preconditions

- ELITEA Chat is accessible
- Artifact Toolkit is configured with a writable bucket
- Jira toolkit is configured with valid credentials and has 'Add file to issue description' tool enabled
- A valid Jira issue key is available (e.g., PROJ-123)
- A local file (e.g., bug-screenshot.png) is available for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Ensure Artifact Toolkit and Jira toolkit are connected | Both toolkits are active in the current Chat session |
| 2 | Use the paperclip button to upload a local file (e.g., bug-screenshot.png) and send a prompt: 'Save this file to /my-bucket/bug-screenshot.png' | File is saved to the Artifact bucket; Chat confirms the path |
| 3 | Send a follow-up prompt: 'Upload /my-bucket/bug-screenshot.png to the Description field of Jira issue [issue_key]' | Chat invokes 'Add file to issue description' tool and reports success |
| 4 | Navigate to Jira and open the issue | bug-screenshot.png appears in the Description field of the Jira issue |

## Expected Final State

bug-screenshot.png appears in the Description field of the Jira issue

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
