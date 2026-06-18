---
id: ELITEA-0432
title: "Chat + Upload → Jira: User-Uploaded File Uploaded to Issue Comment"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:image-generation, integration:jira, feat:toolkits, chat]
requirements: [3180]
---
# ELITEA-0432: Chat + Upload → Jira: User-Uploaded File Uploaded to Issue Comment

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a file uploaded by the user via the Chat paperclip is saved to an Artifact bucket and can be uploaded to a Comment on a Jira issue.

## Preconditions

- ELITEA Chat is accessible
- Artifact Toolkit is configured with a writable bucket
- Jira toolkit is configured with valid credentials and has the upload tool enabled
- A valid Jira issue key is available (e.g., PROJ-123)
- A local file (e.g., workflow.png) is available for upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to ELITEA Chat. Ensure Artifact Toolkit and Jira toolkit are connected | Both toolkits are active in the current Chat session |
| 2 | Use the paperclip button to upload a local file (e.g., workflow.png) and send a prompt: 'Save this file to /my-bucket/workflow.png' | File is saved to the Artifact bucket; Chat confirms the path |
| 3 | Send a follow-up prompt: 'Upload /my-bucket/workflow.png as a comment on Jira issue [issue_key]' | Chat invokes the upload tool targeting the Jira issue Comment and reports success |
| 4 | Navigate to Jira and open the issue, check the Comments section | workflow.png appears in a comment on the Jira issue |

## Expected Final State

workflow.png appears in a comment on the Jira issue

## Pass/Fail Criteria

**Pass:** All steps complete as expected.

**Fail:** Any step produces an unexpected result or error.
