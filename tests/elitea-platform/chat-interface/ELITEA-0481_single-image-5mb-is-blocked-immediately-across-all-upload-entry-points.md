---
id: ELITEA-0481
title: "Single Image >5MB Is Blocked Immediately Across All Upload Entry Points"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0481: Single Image >5MB Is Blocked Immediately Across All Upload Entry Points

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that uploading a single image exceeding 5MB is blocked at the client side immediately — before any LLM call — for every supported upload method (file picker, drag & drop, copy/paste).

**Coverage:**
- File picker upload of a single image >5MB is rejected immediately
- Drag & drop of a single image >5MB onto the chat input area is rejected immediately
- Copy/paste of an image >5MB from clipboard into the chat input is rejected immediately
- No LLM call is triggered for any rejected oversized image
- The rejected image does not appear in the attachment preview list

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Chat conversation with file/image attachment enabled is open (no Agent participant required)
- Test image file prepared: *.jpg (a .jpg image confirmed to exceed 5MB)
- Browser: Chrome (latest) or Firefox (latest)

## Test Data

- Oversized image file: *.jpg (>5MB)
- For copy/paste: copy a >5MB image to clipboard (e.g., screenshot or saved file via right-click → copy)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a new or existing Chat conversation. Confirm the attachment/file-upload button is visible in the chat input area. | Chat input area is visible with an attachment button enabled. |
| 2 | Click the attachment button (file picker). In the OS file dialog, select *.jpg (>5MB). | The OS file dialog opens. File is selectable. |
| 3 | Observe the chat input area after file selection. | *.jpg does NOT appear in the attachment preview. An error/warning message is displayed referencing the 5MB limit. No file is sent. |
| 4 | Without refreshing the page, drag *.jpg from the OS file explorer and drop it directly onto the chat input area. | The dropped file is rejected. The file does NOT appear in the attachment preview. The same (or equivalent) 5MB limit error message is displayed. |
| 5 | Copy a >5MB image to the system clipboard (e.g., right-click → Copy Image on a large image file). Click inside the chat input area and press Ctrl+V to paste. | The pasted image is rejected. The image does NOT appear as an attachment. A 5MB limit error is displayed. |
| 6 | For each of the three rejection attempts, confirm that no message was sent and that clicking Send (if available) does not include the oversized image. | Message is sendable only without the rejected attachment. No oversized image is delivered to the LLM. |

## Expected Final State

Message is sendable only without the rejected attachment. No oversized image is delivered to the LLM.

## Pass/Fail Criteria

**Pass:**
- All three upload methods (picker, drag & drop, paste) correctly block the >5MB image
- Error message appears for each attempt referencing the 5MB limit
- No oversized image appears in the attachment preview or is sent to the LLM

**Fail:**
- The image is accepted by any one upload method (even without appearing to send)
- An LLM response referencing the image content is returned
- No error message is shown after any upload attempt
- The "Internal SDK Error" (or any cryptic server error) appears instead of the client-side 5MB error
