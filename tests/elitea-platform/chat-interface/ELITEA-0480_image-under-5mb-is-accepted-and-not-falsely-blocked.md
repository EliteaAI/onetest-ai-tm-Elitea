---
id: ELITEA-0480
title: "Image Under 5MB Is Accepted and Not Falsely Blocked"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0480: Image Under 5MB Is Accepted and Not Falsely Blocked

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that an image file whose size is less than 5MB is accepted by the attachment system and processed normally — the 5MB enforcement must not falsely block valid images.

**Coverage:**
- Image of ~1MB is accepted without error
- Image of ~4MB is accepted without error
- Both accepted images are sent to the LLM and the AI can respond to them
- No false-positive 5MB error is raised for images under the limit

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Chat conversation with file/image attachment enabled is open
- Test image files prepared:
  - small_image.jpg (~1MB)
  - medium_image.png (~4MB, confirmed under 5MB)

## Test Data

- small_image.jpg (~1MB)
- medium_image.png (~4MB)
- Chat message to send: "Describe what is in this image."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with attachment support. Click the attachment button and select small_image.jpg (~1MB). | small_image.jpg appears in the attachment preview area. No error is shown. |
| 2 | Type the message "Describe what is in this image." and click Send. | Message is sent successfully with the image attachment. The AI responds with a description of the image content. |
| 3 | In the same or a new conversation, click the attachment button and select medium_image.png (~4MB). | medium_image.png appears in the attachment preview area. No error is shown. |
| 4 | Type the message "Describe what is in this image." and click Send. | Message is sent successfully with the image attachment. The AI responds with a description of the image content. |
| 5 | Confirm that in neither attempt did a 5MB limit error appear. | No "exceeds 5 MB" or similar error is displayed for either file. |

## Expected Final State

No "exceeds 5 MB" or similar error is displayed for either file.

## Pass/Fail Criteria

**Pass:**
- Both images (~1MB and ~4MB) are accepted and attached without errors
- Both images are successfully processed by the AI and a response is returned
- No 5MB-related error appears for either file

**Fail:**
- Either image under 5MB triggers a 5MB limit error message
- Either image fails to attach or send
- The AI does not respond to a successfully sent image
