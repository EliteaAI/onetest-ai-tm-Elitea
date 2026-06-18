---
id: ELITEA-0473
title: "5MB Limit Enforced When Adding Image Attachment to Agent Configuration"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, agents]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0473: 5MB Limit Enforced When Adding Image Attachment to Agent Configuration

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the 5MB image size limit is enforced when a user attempts to attach an image directly to an Agent's configuration (e.g., via the Agent editor/builder page), not just in live chat conversations.

## Preconditions

- Logged in to {{base_url}} with a valid user account
- The Agent creation or edit page is open
- Test image files prepared:
  - valid_image.jpg (~2MB, under limit)
  - large_image.jpg (~8MB, over limit)

## Test Data

- valid_image.jpg (~2MB)
- large_image.jpg (~8MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent creation or edit page. Locate the image/file attachment option in the Agent configuration UI. | The attachment option is visible and accessible. |
| 2 | Click the attachment button and select large_image.jpg (~8MB). | The file is rejected. A 5MB limit error message is displayed. The file does NOT appear in the agent's attachment area. |
| 3 | Confirm no change is saved to the agent configuration for the oversized image. | The agent configuration does not include the rejected image. |
| 4 | Click the attachment button and select valid_image.jpg (~2MB). | The file is accepted. It appears in the agent's attachment area or configuration preview. No error is shown. |
| 5 | Save the agent configuration. | Agent is saved successfully with valid_image.jpg attached. |

## Expected Final State

Agent is saved successfully with valid_image.jpg attached.

## Pass/Fail Criteria

Pass:
- Oversized image (>5MB) is rejected in the Agent configuration page with the 5MB error
- Valid image (<5MB) is accepted and saved in the Agent configuration
- Behavior mirrors the 5MB enforcement in chat

Fail:
- Oversized image is accepted and saved in the Agent configuration without error
- No error message appears for an oversized image during agent setup
- Valid image is incorrectly rejected in the Agent configuration
