---
id: ELITEA-0477
title: "Non-Image Files Up to 150MB Are Not Affected by the 5MB Limit"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, regression, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0477: Non-Image Files Up to 150MB Are Not Affected by the 5MB Limit

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the 5MB validation limit applies exclusively to image file types (.jpg, .jpeg, .png, .gif, .webp) and that non-image files (PDF, DOCX, TXT, etc.) continue to be accepted under the existing 150MB limit without any regression.

**Coverage:**
- PDF file >5MB but <150MB is accepted without triggering the 5MB image limit error
- DOCX file >5MB but <150MB is accepted without triggering the 5MB image limit error
- TXT file is accepted normally
- No 5MB error is shown for any non-image file type
- Non-image files can be sent and processed by the AI

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Chat conversation with file attachment enabled is open
- Test files prepared:
  - document.pdf (~100MB)
  - report.docx (~10MB)
  - notes.txt (~6MB)

## Test Data

- document.pdf (~100MB)
- report.docx (~10MB)
- notes.txt (~6MB)
- Chat message: "Summarize this document."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with attachment support. Click the attachment button and select document.pdf (~100MB). | document.pdf appears in the attachment preview. No 5MB error message is shown. |
| 2 | Type "Summarize this document." and click Send. | Message sends successfully. The AI returns a summary or acknowledgment of the PDF content. |
| 3 | In the same or a new conversation, attach report.docx (~10MB). | report.docx appears in the attachment preview. No 5MB error message is shown. |
| 4 | Send a message with report.docx attached. | Message sends successfully with the DOCX file attached. |
| 5 | Attach notes.txt (~6MB) and send a message. | File is accepted. Message sends. AI responds to the TXT content. |
| 6 | Confirm that across all three files, no "5 MB limit" or image-related error was triggered. | No 5MB error appears in any of the three upload attempts. |

## Expected Final State

No 5MB error appears in any of the three upload attempts.

## Pass/Fail Criteria

**Pass:**
- All three non-image files are accepted and attached without triggering a 5MB error
- Files can be sent and the AI processes them
- No regression in non-image file attachment behavior

**Fail:**
- Any non-image file triggers the "Image exceeds 5 MB limit" error
- Any non-image file fails to attach when it is within the 150MB limit
- The 5MB restriction is applied to file types other than images
