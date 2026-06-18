---
id: ELITEA-0472
title: "5MB Image Limit Enforced When Calling Agent Participant (Attachments Tool) via @Mention in Chat Conversation"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:attachments, file-validation, image-upload, agents, chat]
requirements: [ProjectAlita/projectalita.github.io#3624]
---
# ELITEA-0472: 5MB Image Limit Enforced When Calling Agent Participant (Attachments Tool) via @Mention in Chat Conversation

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the 5MB image upload limit is enforced when a user attaches an image while invoking an agent participant (with the `attachments` internal tool enabled) via @mention inside a Chat → Conversation. This flow is distinct from a standalone agent chat: the agent is added as a participant to an existing conversation and called explicitly.

**Coverage:**
- An agent with `attachments` enabled in `internal_tools` can be added as a participant to a Chat Conversation
- Attaching an oversized image (>5MB) while @mentioning the agent is rejected with the 5MB error before the agent is called
- Attaching a valid image (<5MB) while @mentioning the agent is accepted and the agent processes the image correctly
- The 5MB validation behaviour is consistent regardless of whether the agent is the sole participant or added to an existing conversation

## Preconditions

- Logged in to {{base_url}} with a valid user account
- An Agent with `attachments` included in `internal_tools` exists and is accessible
- Navigate to Chat → Conversations and open or create a conversation
- Add the above agent as a participant to the conversation
- Test image files prepared:
  - valid_image.jpg (~2MB, under limit)
  - large_image.jpg (~8MB, over limit)

## Test Data

- valid_image.jpg (~2MB)
- large_image.jpg (~8MB)
- Agent name: any agent with `attachments` enabled in `internal_tools`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat → Conversations. Open an existing conversation or create a new one. | Conversation view opens with the chat input area visible. |
| 2 | Add the agent (with `attachments` in `internal_tools`) as a participant to the conversation via the Participants panel or equivalent UI. | The agent appears in the participants list for the conversation. |
| 3 | In the chat input area, type @[AgentName] to invoke the agent. Before sending, click the attachment button and select large_image.jpg (~8MB). | The file is rejected immediately. A 5MB limit error message is displayed. The file does NOT appear in the attachment preview. The typed @mention remains in the input. |
| 4 | Confirm that no agent call was triggered: the agent has not replied with any content referencing the oversized image. | No response from the agent participant appears in the conversation. |
| 5 | In the chat input area, type @[AgentName] again to invoke the agent. Click the attachment button and select valid_image.jpg (~2MB). | The file appears in the attachment preview. No error is shown. |
| 6 | Add a message (e.g., "Describe this image.") and click Send. | Message is sent with valid_image.jpg attached. The invoked agent responds with a description of the image content. |
| 7 | Confirm in the conversation history that the reply came from the agent participant and that the oversized-image rejection left no partial state in the conversation. | The agent's reply is attributed to the agent participant. No residual error or broken state is visible in the conversation. |

## Expected Final State

The agent's reply is attributed to the agent participant. No residual error or broken state is visible in the conversation.

## Pass/Fail Criteria

**Pass:**
- Oversized image (>5MB) is rejected with the 5MB error when the user attaches it while @mentioning the agent in a Chat Conversation
- No agent call is made for the rejected image
- Valid image (<5MB) is accepted and the agent participant processes it correctly
- Conversation state remains clean after a rejection attempt

**Fail:**
- Oversized image is accepted when the user @mentions the agent in a Chat Conversation
- No 5MB error appears for the oversized image in this flow
- Valid image fails to be processed by the agent participant
- A rejection attempt corrupts conversation state or causes the agent participant to become unresponsive
