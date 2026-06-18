---
id: ELITEA-0479
title: "Error Message Contains Correct Filename and Size for Single Oversized Image"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0479: Error Message Contains Correct Filename and Size for Single Oversized Image

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a single image exceeding 5MB is rejected, the error message displayed to the user contains the specific filename and the actual file size, matching the format specified in the issue.

**Coverage:**
- Error message is shown immediately upon rejection
- Error message contains the rejected file's name (dynamic, not hardcoded)
- Error message contains the rejected file's actual size in MB
- Error message references the 5MB limit
- Error message format matches: "⚠️ Image exceeds 5 MB limit. File: [filename] ([size] MB)"

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Chat conversation with file/image attachment enabled is open
- Two oversized image files prepared with known exact file sizes:
  - screenshot.png (~13.2MB)
  - vacation_photo.jpg (~8.5MB)

## Test Data

- screenshot.png (~13.2MB)
- vacation_photo.jpg (~8.5MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with attachment support. Click the attachment button and select screenshot.png (~13.2MB). | File is rejected. An error message appears. |
| 2 | Read the error message carefully. Verify it contains: (a) a reference to "5 MB limit", (b) the filename screenshot.png, and (c) the file size (approximately 13.2 MB). | The error message shows all three elements. The filename and size in the message match the actual file selected. |
| 3 | Dismiss or close the error. Click the attachment button again and select vacation_photo.jpg (~8.5MB). | File is rejected. A new error message appears. |
| 4 | Verify the new error message now shows: (a) a reference to "5 MB limit", (b) the filename vacation_photo.jpg, and (c) the file size (approximately 8.5 MB). | The filename in the error has changed to vacation_photo.jpg — confirming the filename is dynamically taken from the selected file, not hardcoded. |

## Expected Final State

The filename in the error has changed to vacation_photo.jpg — confirming the filename is dynamically taken from the selected file, not hardcoded.

## Pass/Fail Criteria

**Pass:**
- Error appears immediately for each rejected file
- Error message contains the correct dynamic filename for each attempt
- Error message contains the file size (accurate to at least one decimal place)
- Error message references the 5MB limit

**Fail:**
- Error message does not appear
- Error message shows a generic text without the filename or size
- The same filename appears regardless of which file is selected (hardcoded)
- Error message reads "Internal SDK Error" or any generic server error
