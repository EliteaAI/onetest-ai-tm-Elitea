---
id: ELITEA-0471
title: "Chat Conversation with Agent Carrying Pre-Configured Image Attachment"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, agents, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0471: Chat Conversation with Agent Carrying Pre-Configured Image Attachment

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a user starts a chat conversation with an Agent that has a pre-configured image attachment (<5MB) in its configuration, the agent loads and responds correctly — and that the 5MB limit is still enforced for any additional images the user tries to attach during the conversation.

**Coverage:**
- An Agent with a valid pre-configured image attachment (<5MB) loads correctly in chat
- The pre-configured image is accessible to the agent during the conversation
- Attaching an additional oversized image (>5MB) in the chat with this agent is still rejected
- Attaching an additional valid image (<5MB) in the chat with this agent is accepted

## Preconditions

- Logged in to {{base_url}} with a valid user account
- An Agent has been configured with a valid image attachment (valid_image.jpg, ~2MB) saved in its configuration (see TC-NEW-14 / TC-0581 setup)
- A Chat conversation is open with this Agent as a participant
- Additional test image files prepared:
  - user_valid.jpg (~1MB, under limit)
  - user_large.jpg (~8MB, over limit)

## Test Data

- Agent pre-configured with: valid_image.jpg (~2MB)
- user_valid.jpg (~1MB) — to attach during chat
- user_large.jpg (~8MB) — to attempt attaching during chat

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with the Agent that has valid_image.jpg pre-configured. Send an initial message (e.g., "Hello, describe your configured image."). | The Agent responds correctly. No error is shown on load. The pre-configured image is available to the agent context. |
| 2 | In the chat input area, click the attachment button and select user_large.jpg (~8MB). | The file is rejected. A 5MB limit error message is displayed. The file does NOT appear in the attachment preview. |
| 3 | Confirm the agent's pre-configured image context is unaffected by the rejection. | The agent continues to function normally; no session error is triggered. |
| 4 | Click the attachment button and select user_valid.jpg (~1MB). | The file is accepted. It appears in the attachment preview. No error is shown. |
| 5 | Send a message with user_valid.jpg attached (e.g., "Also describe this new image."). | Message sends successfully. The Agent responds to the newly attached image. |

## Expected Final State

Message sends successfully. The Agent responds to the newly attached image.

## Pass/Fail Criteria

**Pass:**
- Agent with pre-configured image attachment loads and responds correctly in chat
- Oversized image (>5MB) attached by the user during chat is rejected with the 5MB error
- Valid image (<5MB) attached by the user during chat is accepted and processed by the Agent
- Pre-configured image context is not disrupted by a rejected upload attempt

**Fail:**
- Agent fails to load in chat when it has a pre-configured image attachment
- Oversized image attached during chat is accepted without error
- A rejection during chat causes the agent session or pre-configured context to break
- Valid user-attached image fails to be processed by the agent
