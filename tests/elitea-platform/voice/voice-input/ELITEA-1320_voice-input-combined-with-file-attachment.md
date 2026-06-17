---
id: ELITEA-1320
title: "Voice Input Combined With File Attachment"
priority: high
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [nfr:accessibility, feature:4499, integration, attachment, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1320: Voice Input Combined With File Attachment

**Module:** Voice Input · **Priority:** High · **Type:** Functional

**Objective:** Verify that voice-dictated text and a file attachment can be combined in the same chat message and both are submitted and processed correctly.

**Coverage:**
- File attachment can be added to the input field and coexists with active voice recording
- Transcribed text is not affected by the presence of an attachment
- Both the text and file are present in the input field before submission
- Both the text and file are visible in the chat history after submission

## Preconditions

- User is logged into ELITEA
- ASR model configured in the project
- Chat page open
- Microphone permission granted
- A small file is available for upload (e.g. test.txt — any supported format)
- Browser: Chrome or Edge

## Test Data

- Attachment file: test.txt (any small text file)
- Spoken phrase: "Please analyze this file"
- Expected input state before submit: text "Please analyze this file" + file chip visible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the attachment button in the chat input toolbar. Select and attach test.txt. | The file attachment is shown in the input area (file chip/preview is visible). |
| 2 | Click the microphone icon to start recording. | Recording starts. The attached file chip remains visible alongside the active recording state. |
| 3 | Speak "Please analyze this file". Pause. Click the microphone icon to stop recording. | Transcribed text "Please analyze this file" appears in the input field. The file attachment is still present. |
| 4 | Click the Send button to submit the message. | The message with both the transcribed text and the file attachment is submitted. Both are visible in the chat history entry. |

## Expected Final State

The message with both the transcribed text and the file attachment is submitted. Both are visible in the chat history entry.

## Pass/Fail Criteria

**Pass:**
- Attachment remains intact after the recording session
- Both transcribed text and file attachment appear in the input field before send
- Both text and file are submitted and visible in chat history after send

**Fail:**
- Attachment is lost or removed when recording starts or stops
- Only the text or only the file is submitted — not both
- Input field crashes, throws an error, or behaves unexpectedly when both attachment and recording are used together
