---
id: ELITEA-0309
title: "Chat Attachment - Files Uploaded to Bucket Folders Are Accessible in Chat"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [integration, attachment, regression, artifacts, chat, p1]
requirements: [ProjectAlita/projectalita.github.io#3386]
---
# ELITEA-0309: Chat Attachment - Files Uploaded to Bucket Folders Are Accessible in Chat

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify that files uploaded to bucket subfolders can be discovered and attached in Chat conversations, ensuring the cross-feature integration between Artifacts and Chat is intact.

**Coverage:**
- Artifact files from folder paths are accessible in the Chat file attachment browser
- Files can be selected and attached to a chat message
- Attached folder-path file is referenced correctly in the sent message

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium
- A text file has been uploaded to a bucket folder path (e.g., test/data.txt in bucket 'excel')
- A Chat conversation exists and the 'attach files' button is available

## Test Data

- URL: {{base_url}}
- Bucket: excel
- File in folder: test/data.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open or create a conversation. | Chat interface is loaded. |
| 2 | Click the 'attach files' button in the chat input area. | File attachment browser or picker opens. |
| 3 | Browse to the Artifacts section, select bucket 'excel', and navigate into folder 'test'. | Folder contents are accessible showing data.txt. |
| 4 | Select data.txt and confirm the attachment. | data.txt is attached to the chat message input. |
| 5 | Send the message with the attachment. | Message is sent. Attachment is visible in the conversation without errors. |

## Expected Final State

Message is sent. Attachment is visible in the conversation without errors.

## Pass/Fail Criteria

**Pass:**
- Files from bucket subfolders are visible in the Chat file attachment browser
- File can be selected, attached, and sent in a chat message
- No errors or broken references for folder-path files

**Fail:**
- Folder-path files are not listed in the attachment browser
- Attaching a folder-path file causes an error
- Attached file cannot be resolved or displayed in the chat
