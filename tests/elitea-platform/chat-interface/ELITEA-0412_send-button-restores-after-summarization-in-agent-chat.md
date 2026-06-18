---
id: ELITEA-0412
title: "Send Button Restores After Summarization in Agent Chat"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:context-management, feat:chat, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3984]
---
# ELITEA-0412: Send Button Restores After Summarization in Agent Chat

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when auto-summarization is triggered in an Agent chat conversation, the Terminate button reverts to Send after generation completes — confirming the fix is not limited to direct LLM chat.

**Coverage:**
- Auto-summarization in Agent chat context
- Send button state restoration after Agent completes response post-summarization
- Agent conversation remains fully functional after restoration

## Preconditions

- Logged in to {{base_url}} with Editor/Admin role
- `context_manager` secret = `true`; Summarization toggle = ON
- At least one Agent exists configured with Claude Opus 4.5 or GPT-4.1
- Browser: Chrome (latest)

## Test Data

- Agent: any existing agent with Claude Opus 4.5 or GPT-4.1
- Context-filling message: "Provide a comprehensive detailed analysis of the history of jazz music from 1900 to the present day including all major sub-genres, key artists, and cultural impact"
- Follow-up (to trigger summarization): "Now extend this analysis to include the influence of jazz on modern hip-hop and R&B"
- Post-restoration message: "Summarize what we discussed"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents, open an existing agent configured with Claude Opus 4.5 or GPT-4.1. | Agent chat interface is open. |
| 2 | Start a chat session with the agent. | Agent chat input is visible. |
| 3 | Send the context-filling message. | Terminate button appears; Agent generates a long response. |
| 4 | Observe the Context Budget widget — confirm token usage reaches ≥ 100%. | Widget indicator is orange. |
| 5 | Send the follow-up message: 'Now extend this analysis to include the influence of jazz on modern hip-hop and R&B'. | Terminate button appears during generation. |
| 6 | Confirm a summarization event occurs (Summaries count increments in the widget). | Summaries count > 0. |
| 7 | Wait for the Agent's full response to complete after the summarization. | Full response is shown in the chat. |
| 8 | Observe the chat input immediately after the response completes. | Send button is displayed — not Terminate. |
| 9 | Type 'Summarize what we discussed' and click Send. | Message is sent successfully. |
| 10 | Confirm the button cycles correctly: Send → Terminate (during generation) → Send (after completion). | Full cycle completes without getting stuck. |

## Expected Final State

Full cycle completes without getting stuck.

## Pass/Fail Criteria

**Pass:**
- Send button displayed after Agent completes response post-summarization
- Follow-up messages can be sent normally using the restored Send button
- Button cycles correctly through Send → Terminate → Send on each new message

**Fail:**
- Terminate button remains after Agent completes response post-summarization
- Button stuck in Terminate state, preventing new messages
