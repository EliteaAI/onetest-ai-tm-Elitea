---
id: ELITEA-0118
title: "Regenerate After Image Attachment in Agent Chat"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:attachments, feat:agents]
requirements: [ProjectAlita/projectalita.github.io#3591]
---
# ELITEA-0118: Regenerate After Image Attachment in Agent Chat

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Regenerate button works correctly after sending an image attachment in the Agents section — triggering a new generation rather than silently returning the same response.

**Coverage:**
- Regenerate after image attachment as the first message in agent chat (minimum 1 image)
- Regenerate after image attachment as the first message in agent chat (maximum 10 images)
- Regenerate after image attachment as a non-first message in agent chat (minimum 1 image)
- Regenerate after image attachment as a non-first message in agent chat (maximum 10 images)
- Supported image formats: .jpg/.jpeg, .png, .gif (first frame only), .bmp, .webp, .svg, .tiff/.tif, .ico, .apng, .avif

## Preconditions

- User is logged in to {{base_url}} — Private project active
- An agent is configured with "Allow attachments" toggle enabled and an Artifact bucket assigned in the Configuration tab
- The agent uses a vision-capable model (e.g., Claude Sonnet, GPT-4o)
- Test image files prepared: at least 10 image files (JPEG or PNG recommended), each < 150 MB, total batch < 150 MB

## Test Data

Parametrization table:
| # | Message Position   | Image Quantity       |
|---|--------------------|----------------------|
| 1 | First message      | 1 image (minimum)    |
| 2 | First message      | 10 images (maximum)  |
| 3 | Non-first message  | 1 image (minimum)    |
| 4 | Non-first message  | 10 images (maximum)  |

File specs: each image < 150 MB; total per message < 150 MB
Supported formats: .jpg, .jpeg, .png, .gif, .bmp, .webp, .svg, .tiff, .tif, .ico, .apng, .avif
Text prompt: "Describe this image" (1 file) / "Describe these images" (10 files)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents section from the sidebar and open the configured agent (Allow attachments enabled, Artifact bucket assigned). | Agent chat interface is open and ready to receive input. |
| 2 | Parametrize by message position: - FIRST MESSAGE (variants 1, 2): Ensure the agent chat has no prior messages — open a fresh agent session if needed. - NON-FIRST MESSAGE (variants 3, 4): Send a plain text message (e.g. "Hello") and wait for the agent response before continuing. | First message variants: chat is empty. Non-first message variants: at least one prior exchange exists in the chat. |
| 3 | Click the paperclip (📎) icon in the message input area to open the file picker. | File selection dialog opens. |
| 4 | Attach image files per the active variant: - Variants 1 & 3 (minimum): attach 1 image file - Variants 2 & 4 (maximum): attach 10 image files Supported formats: .jpg/.jpeg, .png, .gif, .bmp, .webp, .svg, .tiff/.tif, .ico, .apng, .avif. Each file < 150 MB; total < 150 MB. | File(s) appear as attachment chips in the message input area. |
| 5 | Type the text prompt: "Describe this image" (for 1 file) or "Describe these images" (for 10 files). | Text prompt is entered alongside the attachment(s). |
| 6 | Click Send and wait for the agent to return a full response. | Agent produces a response referencing or analyzing the attached image(s). |
| 7 | Click the Regenerate (🔄) icon located near the last agent message. | A new generation cycle starts — a loading indicator appears on the last message. |
| 8 | Wait for the regeneration to complete. | A new or refreshed response is produced. Behavior is consistent across all 4 parameter combinations. |

## Expected Final State

A new or refreshed response is produced. Behavior is consistent across all 4 parameter combinations.

## Pass/Fail Criteria

**Pass:**
- Loading indicator appears immediately after clicking Regenerate
- A new or refreshed response is produced
- No error message is displayed
- Behavior is consistent across all 4 parametrization combinations

**Fail:**
- No generation activity occurs after clicking Regenerate
- The same static response is returned silently with no loading indicator
- An error message is displayed
- Regenerate button is unresponsive or disabled
