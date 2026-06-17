---
id: ELITEA-0902
title: "Drag and Drop and Clipboard Paste Work as Attachment Entry Points in Pipeline Chat"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0902: Drag and Drop and Clipboard Paste Work as Attachment Entry Points in Pipeline Chat

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that files can be attached to the pipeline chat via drag and drop and clipboard paste (Ctrl+V), not only via the file picker.

**Coverage:**
- Drag and drop file onto pipeline chat input — file accepted
- Ctrl+V paste of clipboard image — image accepted
- Both methods store file in attachments bucket

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled

## Test Data

- File for drag and drop: doc.pdf
- Clipboard image: screenshot pasted via Ctrl+V

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline test chat. | Chat input is displayed with active paperclip. |
| 2 | Drag doc.pdf from the file system and drop it onto the chat input area. | File is accepted; filename/thumbnail appears in input. No error shown. |
| 3 | Type a prompt and click Send. | Message sent with dragged file. |
| 4 | Copy an image to clipboard (e.g., screenshot). In the chat input, press Ctrl+V. | Image is pasted as an attachment thumbnail in the input. |
| 5 | Type a prompt and click Send. | Message sent with pasted image. |
| 6 | Navigate to Artifacts → attachments bucket. | Both files (doc.pdf and pasted screenshot) appear in the bucket. |

## Expected Final State

Both files (doc.pdf and pasted screenshot) appear in the bucket.

## Pass/Fail Criteria

**Pass:**
- Drag and drop accepted without error
- Ctrl+V paste accepted without error
- Both files stored in attachments bucket

**Fail:**
- Drag and drop silently ignored or errors
- Paste not recognized as attachment
