---
id: ELITEA-0416
title: "Send Button Restores After Multiple Consecutive Summarizations in Direct Chat"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:context-management, feat:chat, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3984]
---
# ELITEA-0416: Send Button Restores After Multiple Consecutive Summarizations in Direct Chat

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Terminate button correctly reverts to Send after each of multiple consecutive summarization events within the same Chat conversation — covering the intermittent floating-bug scenario.

**Coverage:**
- Two or more sequential summarization events in the same conversation
- Send button state restored after each summarization event
- No permanent Terminate lock after N summarizations

## Preconditions

- Logged in to {{base_url}} with Editor/Admin role
- `context_manager` secret = `true`; Summarization toggle = ON
- Context Budget configured to reliably trigger summarization within a manageable number of messages
- Browser: Chrome (latest)

## Test Data

- Model: Claude Opus 4.5 or GPT-4.1
- Message series (send 3–4 to fill context and repeatedly trigger summarization):
  1. "Give me an exhaustive biography of The Red Hot Chili Peppers"
  2. "Now give me a detailed history of rock music from 1950 to 2000"
  3. "List every studio album by Led Zeppelin with full track listings and descriptions"
  4. "Write a comprehensive essay on the evolution of electric guitar technology"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new direct LLM chat conversation and select Claude Opus 4.5. | Blank conversation is open. |
| 2 | Send message 1: 'Give me an exhaustive biography of The Red Hot Chili Peppers'. Wait for the full response. | Response received; context usage is visible in the widget. |
| 3 | Observe the Context Budget — confirm token usage is at or near 100%. | Widget indicator is orange. |
| 4 | Send message 2: 'Now give me a detailed history of rock music from 1950 to 2000'. | Generation starts; Terminate button is visible. |
| 5 | Observe the Context Budget — confirm a first summarization event occurs (Summaries count = 1). | Summaries count increments to 1. |
| 6 | Wait for the full response to complete after the first summarization. | Full response is displayed. |
| 7 | Immediately observe the chat input. | Send button is shown — not Terminate. |
| 8 | Send message 3: 'List every studio album by Led Zeppelin with full track listings and descriptions' to trigger a second summarization. | Terminate button appears; another summarization event occurs (Summaries count = 2). |
| 9 | Wait for the response to complete. | Full response displayed. |
| 10 | Confirm the Send button is restored again after the second summarization. | Send button displayed — not Terminate. |
| 11 | If Terminate remains at step 7 or 10, send one more message and document whether the button recovers or stays stuck permanently. | Document recovery or permanent lock state. |

## Expected Final State

Document recovery or permanent lock state.

## Pass/Fail Criteria

**Pass:**
- Send button is restored after every summarization event regardless of how many have occurred
- No permanent Terminate lock after multiple summarizations

**Fail:**
- Terminate button remains after any summarization event (first, second, or subsequent)
- Button enters a permanently non-responsive state requiring page reload
