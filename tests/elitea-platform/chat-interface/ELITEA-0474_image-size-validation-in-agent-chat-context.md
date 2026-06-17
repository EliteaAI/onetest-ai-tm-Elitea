---
id: ELITEA-0474
title: "Image Size Validation in Agent Chat Context"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0474: Image Size Validation in Agent Chat Context

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the 5MB image upload restriction is enforced in Agent-based Chat conversations (where an Agent with attachments in internal_tools is a participant), not only in standalone Chat conversations.

## Preconditions

- Logged in to {{base_url}} with a valid user account
- An Agent is configured with attachments included in internal_tools
- A Chat conversation is open with this Agent as a participant
- Test image files prepared:
  - valid_image.jpg (~2MB, under limit)
  - large_image.jpg (~8MB, over limit)

## Test Data

- valid_image.jpg (~2MB)
- large_image.jpg (~8MB)
- Agent name: any agent with attachments enabled in internal tools

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation that includes an Agent with attachments enabled. Confirm the attachment button is active in the chat input area. | Chat input with attachment button is visible. |
| 2 | Click the attachment button and select large_image.jpg (~8MB). | The file is rejected. A 5MB limit error message is displayed. The file does NOT appear in the attachment preview. |
| 3 | Confirm no LLM/Agent call was triggered for the rejected image. | No Agent response referencing the oversized image content is returned. |
| 4 | Click the attachment button and select valid_image.jpg (~2MB). | The file appears in the attachment preview. No error is shown. |
| 5 | Type a message ("Describe this image.") and click Send. | Message is sent with valid_image.jpg attached. The Agent responds with a description of the image. |

## Expected Final State

Message is sent with valid_image.jpg attached. The Agent responds with a description of the image.

## Pass/Fail Criteria

Pass:
- Oversized image (>5MB) is correctly rejected in Agent chat with the 5MB error
- Valid image (<5MB) is accepted and the Agent processes it correctly
- Behavior is consistent with plain chat context

Fail:
- Oversized image is accepted in Agent chat (even if rejected in plain chat)
- No error message is shown in Agent chat for an oversized image
- Valid image fails to attach in Agent chat context
