---
id: ELITEA-0478
title: "Mixed Batch Upload: Oversized Images Rejected, Valid Images Proceed"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0478: Mixed Batch Upload: Oversized Images Rejected, Valid Images Proceed

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that when multiple images are uploaded simultaneously and some exceed 5MB, only the oversized images are rejected while valid images under the limit proceed to attachment normally. The error message must list the rejected filenames.

**Coverage:**
- In a batch upload, images <5MB are accepted while images >5MB are rejected
- Valid images appear in the attachment preview; oversized images do not
- Error message lists the specific filenames of rejected images
- Sending the message includes only the valid images
- Partial rejection does not block the valid images from being submitted

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Chat conversation with file/image attachment enabled is open
- A batch of 4 image files prepared:
  - small1.jpg (~1MB, under limit)
  - small2.png (~2MB, under limit)
  - large1.jpg (~8.5MB, over limit)
  - large2.png (~13.2MB, over limit)

## Test Data

- small1.jpg (~1MB)
- small2.png (~2MB)
- large1.jpg (~8.5MB)
- large2.png (~13.2MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with attachment support. Click the attachment button and select all 4 files simultaneously (small1.jpg, small2.png, large1.jpg, large2.png) using multi-select in the OS file dialog (Ctrl+Click or Shift+Click). | File selection dialog allows selecting multiple files. |
| 2 | Observe the attachment preview area after file selection. | small1.jpg and small2.png appear in the attachment preview. large1.jpg and large2.png do NOT appear. |
| 3 | Observe the error/notification area. | An error message appears listing the rejected files: large1.jpg and large2.png. The error references the 5MB limit. |
| 4 | Confirm that small1.jpg and small2.png are in the attachment preview unaffected by the rejection of the oversized files. | Both valid images remain in the preview. No error is shown for them. |
| 5 | Type a message (e.g., "Describe these images.") and click Send. | The message is sent. Only small1.jpg and small2.png are included as attachments. The AI responds to the two valid images. |
| 6 | Confirm the rejected images (large1.jpg, large2.png) are not part of the sent message in the conversation history. | Conversation history shows only two image attachments. No trace of the oversized files. |

## Expected Final State

Conversation history shows only two image attachments. No trace of the oversized files.

## Pass/Fail Criteria

**Pass:**
- Valid images (<5MB) attach successfully while oversized images (>5MB) are rejected
- Error message lists both rejected filenames
- Sending the message includes only the valid images
- Valid images are processed by the AI

**Fail:**
- Any oversized image is accepted alongside the valid images
- Both valid and oversized images are rejected entirely (all-or-nothing behavior)
- Error does not list which files were rejected
- The valid images are blocked because oversized images were also selected
