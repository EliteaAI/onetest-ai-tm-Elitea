---
id: ELITEA-0417
title: "Send Button Restores After First Auto-Summarization in Direct Chat"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:context-management, feat:chat, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3984]
---
# ELITEA-0417: Send Button Restores After First Auto-Summarization in Direct Chat

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after a single auto-summarization event completes in a direct LLM chat conversation, the Terminate button reverts to the Send button — allowing the user to continue the conversation.

**Coverage:**
- Context Budget auto-summarization triggers in direct LLM chat
- Terminate button state reverts to Send immediately after model finishes responding post-summarization
- Verified with both Claude Opus 4.5 and GPT-4.1

## Preconditions

- Logged in to {{base_url}} as a user with Editor/Admin role
- `context_manager` project-level secret is set to `true` (Settings → Secrets)
- Context Budget widget is enabled; Summarization toggle is ON (expanded view)
- Browser: Chrome (latest)
- A new direct Chat conversation (no agent participant) is available

## Test Data

- Model A: Claude Opus 4.5; Model B: GPT-4.1
- Trigger message: "Give me an exhaustive biography of The Red Hot Chili Peppers"
- Follow-up message: "Tell me more about their discography"
- Context Budget: default settings (or Max Context Tokens set low enough to be filled within 1–2 messages)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat → Conversations and click + Create to open a new direct LLM conversation. | New blank conversation is open with no participants. |
| 2 | Select Claude Opus 4.5 as the LLM model. | Claude Opus 4.5 is shown as the active model. |
| 3 | Send the trigger message: 'Give me an exhaustive biography of The Red Hot Chili Peppers'. | Terminate button appears during generation; a long response is returned. |
| 4 | Observe the Context Budget widget — confirm token usage reaches or exceeds 100% after the response. | Widget shows token % ≥ 100%, status indicator is orange. |
| 5 | Send the follow-up message: 'Tell me more about their discography'. | Terminate button appears during generation. |
| 6 | Observe the Context Budget widget — confirm a summarization event occurs (Summaries count increments from 0 to ≥ 1). | Summaries count is ≥ 1. |
| 7 | Wait for the LLM to fully complete its response after the summarization step. | Full response is displayed in the conversation. |
| 8 | Immediately observe the chat input area after the response completes. | Send button is displayed — not Terminate. |
| 9 | Repeat steps 1–8 using GPT-4.1. | Same outcome: Send button visible after summarization completes. |

## Expected Final State

Same outcome: Send button visible after summarization completes.

## Pass/Fail Criteria

**Pass:**
- Send button is displayed after every summarization-triggered response completes
- Behavior is consistent for both Claude Opus 4.5 and GPT-4.1
- No user action required to reset the button state

**Fail:**
- Terminate button remains visible after the LLM finishes responding post-summarization
- Button requires page reload or explicit user action to revert
