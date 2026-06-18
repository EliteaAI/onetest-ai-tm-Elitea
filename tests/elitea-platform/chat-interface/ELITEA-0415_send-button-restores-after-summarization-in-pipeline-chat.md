---
id: ELITEA-0415
title: "Send Button Restores After Summarization in Pipeline Chat"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:context-management, feat:chat, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3984]
---
# ELITEA-0415: Send Button Restores After Summarization in Pipeline Chat

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that in a Pipeline chat panel, the Terminate button reverts to Send after auto-summarization completes — confirming consistent button state behavior across all context-managed surfaces.

**Coverage:**
- Auto-summarization triggered in Pipeline chat context
- Send button state restoration in Pipeline chat panel
- Pipeline remains functional for new input after button restoration

## Preconditions

- Logged in to {{base_url}} with Editor/Admin role
- `context_manager` secret = `true`; Summarization toggle = ON
- A Pipeline exists with an LLM node supporting multi-turn conversation
- Browser: Chrome (latest)

## Test Data

- Pipeline: any pipeline with an LLM or Agent node using Claude Opus 4.5 or GPT-4.1
- Context-filling messages: 3–4 large-content messages (e.g., "Give me an exhaustive biography of The Red Hot Chili Peppers", "Now give me a detailed history of rock music from 1950 to 2000", "List every studio album by Led Zeppelin with full track listings")
- Follow-up: "Continue the analysis"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines, open a pipeline with a chat panel interface. | Pipeline chat panel is accessible. |
| 2 | Send the first large-content message. | Terminate button appears; pipeline processes and responds. |
| 3 | Continue sending messages until the Context Budget widget shows ≥ 100%. | Widget indicator turns orange. |
| 4 | Send a follow-up message and wait for processing. | Terminate button is visible during processing. |
| 5 | Confirm a summarization event occurs (Summaries count increments). | Summaries count > 0. |
| 6 | Wait for the pipeline to fully complete its response after the summarization step. | Full response is displayed in the pipeline chat panel. |
| 7 | Observe the chat input area. | Send button is displayed — not Terminate. |
| 8 | Send an additional message: 'Continue the analysis'. Confirm Send → Terminate → Send cycle. | Pipeline responds and button cycles correctly. |

## Expected Final State

Pipeline responds and button cycles correctly.

## Pass/Fail Criteria

**Pass:**
- Send button displayed after pipeline completes response post-summarization
- New messages processed correctly after button restoration
- Button cycles: Send → Terminate → Send without getting stuck

**Fail:**
- Terminate button remains in the pipeline chat panel after summarization completes
- User cannot send new messages to the pipeline
