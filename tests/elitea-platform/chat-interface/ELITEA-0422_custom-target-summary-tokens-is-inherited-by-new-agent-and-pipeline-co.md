---
id: ELITEA-0422
title: "Custom Target Summary Tokens Is Inherited by New Agent and Pipeline Conversations"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:context-management, feat:personalization, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3929]
---
# ELITEA-0422: Custom Target Summary Tokens Is Inherited by New Agent and Pipeline Conversations

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that the custom Target Summary Tokens value set in Personalization also propagates to new Agent chat conversations and new Pipeline chat sessions — not only to direct Chat conversations.

**Coverage:**
- Target Summary Tokens (200) is correctly inherited in new Chat conversations
- Target Summary Tokens (200) is correctly inherited in new Agent chat conversations
- Target Summary Tokens (200) is correctly inherited in new Pipeline chat sessions

## Preconditions

- User logged in at {{base_url}}
- Private project selected
- Both "Enable context management for new conversations" and "Enable automatic summarization" are ON in Personalization
- Target Summary Tokens set to 200 in Personalization and saved
- At least one Agent exists in the Private project
- At least one Pipeline exists in the Private project

## Test Data

- Target Summary Tokens in Personalization: 200
- Test Agent: any available agent in Private project
- Test Pipeline: any available pipeline in Private project
- Verification message text: "Hello"

| Conversation type | Expected Target Summary Tokens |
|---|---|
| Chat | 200 |
| Agent chat | 200 |
| Pipeline chat | 200 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/user-settings/profile. Expand 'Default Summarization'. Set Target Summary Tokens to 200. Click Save. | Save succeeds. Target Summary Tokens is 200. |
| 2 | Navigate to Chat. Click Create to open a new conversation. Send the message 'Hello'. | Message is sent, AI responds, Context Budget widget appears. |
| 3 | Click 'Edit context settings' on the Context Budget widget. Expand the Summarization section. Read the Target Summary Tokens field. | Target Summary Tokens = 200. Close modal. |
| 4 | Navigate to the Agents page. Open any existing Agent. Start a new chat session (use a new/clear session to ensure a fresh conversation). | Agent chat interface opens with a new/empty session. |
| 5 | Send the message 'Hello' in the Agent chat. Wait for AI response. Confirm the Context Budget widget appears. | Message is sent and responded to. Context Budget widget is visible. |
| 6 | Click 'Edit context settings' on the Context Budget widget in the Agent chat. Expand the Summarization section. Read the Target Summary Tokens field. | Target Summary Tokens = 200. Close modal. |
| 7 | Navigate to the Pipelines page. Open any existing Pipeline. Access the chat/run panel for a new session. | Pipeline chat interface opens with a new session. |
| 8 | Trigger a run or send a message in the Pipeline chat panel. Wait for the Context Budget widget to appear. | Pipeline executes. Context Budget widget is visible. |
| 9 | Click 'Edit context settings' and find the Target Summary Tokens field in the Summarization section. | Target Summary Tokens = 200. |

## Expected Final State

Target Summary Tokens = 200.

## Pass/Fail Criteria

**Pass:**
- Target Summary Tokens = 200 in the new Chat conversation's Context Management modal
- Target Summary Tokens = 200 in the new Agent chat session's Context Management modal
- Target Summary Tokens = 200 in the new Pipeline chat session's Context Management modal

**Fail:**
- Any of the three conversation types shows Target Summary Tokens = 4096 (default) instead of 200
- Context Budget widget does not appear in Agent or Pipeline chat sessions
- Context Management modal fails to open for any conversation type
