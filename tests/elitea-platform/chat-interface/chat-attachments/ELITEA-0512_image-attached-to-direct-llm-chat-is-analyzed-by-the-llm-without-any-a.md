---
id: ELITEA-0512
title: "Image attached to direct LLM chat is analyzed by the LLM without any artifact toolkit configuration"
priority: critical
type: functional
module: chat-attachments
status: ready
execution_type: manual
tags: [feat:attachments, issue:1285, feat:chat, r-2.0.0b]
requirements: [ProjectAlita/projectalita.github.io#1285]
---
# ELITEA-0512: Image attached to direct LLM chat is analyzed by the LLM without any artifact toolkit configuration

**Module:** Chat Attachments · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that in a direct LLM chat conversation (no agent), attaching a `.jpg` or `.png` image and sending a prompt causes the LLM to analyze it using vision — with no artifact toolkit setup, the file is automatically stored in the default `attachments` bucket.

**Coverage:**
- Paperclip icon is enabled immediately in direct LLM chat with no configuration required
- Image attaches successfully and thumbnail appears in the input field
- LLM returns a natural-language description of the image content
- File appears in the default `attachments` Artifact bucket after sending
- No errors related to missing toolkit or bucket configuration

## Preconditions

- Logged into ELITEA at {{base_url}}
- No artifact toolkit configured
- A `.jpg` image file under 5 MB available locally (e.g., `test_image.jpg`, ~1 MB)

## Test Data

- Image file: `test_image.jpg` (~1 MB, under 5 MB limit)
- Model: any vision-capable model (e.g., GPT-5.2 or Claude Sonnet 3.5)
- Prompt: "Describe what you see in this image"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat from the sidebar → click New Conversation → select any vision-capable model (e.g., GPT-5.2) | Empty chat input is visible; paperclip icon is immediately active and clickable — no configuration or setup required |
| 2 | Click the paperclip icon → select `test_image.jpg` from the file browser | Image thumbnail appears above the message input field; no error message shown |
| 3 | Type "Describe what you see in this image" in the input → click Send | Message is sent with the image attachment |
| 4 | Wait for the AI response | AI returns a natural-language description of the image content; no SDK error, upload failure, or 'missing toolkit' error message appears |
| 5 | Navigate to Artifacts in the sidebar → open the default `attachments` bucket | `test_image.jpg` is present in the `attachments` bucket — confirming automatic storage without any manual artifact toolkit configuration |

## Expected Final State

`test_image.jpg` is present in the `attachments` bucket — confirming automatic storage without any manual artifact toolkit configuration

## Pass/Fail Criteria

**Pass:**
- Paperclip active in direct LLM chat without configuration
- AI describes the image content accurately
- File found in the default `attachments` bucket after sending
- No error messages throughout the flow

**Fail:**
- Paperclip disabled or setup required for direct LLM chat
- Upload fails or AI cannot process the image
- File not found in `attachments` bucket
- Any error message shown
