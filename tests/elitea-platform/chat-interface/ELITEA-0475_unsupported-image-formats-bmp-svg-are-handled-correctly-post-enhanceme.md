---
id: ELITEA-0475
title: "Unsupported Image Formats (.bmp, .svg) Are Handled Correctly Post-Enhancement"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0475: Unsupported Image Formats (.bmp, .svg) Are Handled Correctly Post-Enhancement

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that file formats noted as unsupported by the platform (.bmp, .svg) continue to be rejected for the correct reason (unsupported file type) and are not incorrectly blocked due to the new 5MB image size validation logic.

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Chat conversation with file/image attachment enabled is open
- Two small test files prepared (both confirmed under 5MB):
  - small_image.bmp (~1MB)
  - small_icon.svg (~50KB)

## Test Data

- small_image.bmp (~1MB, unsupported format)
- small_icon.svg (~50KB, unsupported format)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with attachment support. Click the attachment button and select small_image.bmp (~1MB). | The file is rejected. An error message is shown. |
| 2 | Read the error message. Confirm it indicates an unsupported file type reason — NOT a "5 MB limit exceeded" message. | Error message references unsupported type/format, not the 5MB limit. |
| 3 | Click the attachment button and select small_icon.svg (~50KB). | The file is rejected. An error message is shown. |
| 4 | Read the error message. Confirm it indicates an unsupported file type reason — NOT a "5 MB limit exceeded" message. | Error message references unsupported type/format, not the 5MB limit. |
| 5 | Confirm that neither .bmp nor .svg appears in the attachment preview after their respective failed upload attempts. | Neither file appears in the attachment or preview area. |

## Expected Final State

Neither file appears in the attachment or preview area.

## Pass/Fail Criteria

Pass:
- Both .bmp and .svg files are rejected due to unsupported file type
- No "5 MB limit" error is shown for either format (they are under 5MB)
- The error reason is clearly "unsupported type", not a size error

Fail:
- A .bmp or .svg file is accepted and appears in the attachment preview
- The error shown for .bmp or .svg references the 5MB limit (wrong error type)
- No error appears at all for an unsupported format
