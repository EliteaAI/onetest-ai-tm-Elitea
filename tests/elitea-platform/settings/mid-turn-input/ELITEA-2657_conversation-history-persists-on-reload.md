---
id: ELITEA-2657
title: "Verify conversation history with mid-turn messages persists correctly on page reload"
priority: critical
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:chat, eng:backend, eng:frontend, eng:sdk, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6115]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has completed a conversation with mid-turn interaction
- Conversation contains: original message, mid-turn message, agent response

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat/{conversation_id}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note the current conversation state with mid-turn message | Conversation shows original, mid-turn, and response messages |
| 2 | Refresh the page (F5 or browser refresh) | Page reloads |
| 3 | Wait for conversation to load | Conversation history loads completely |
| 4 | Verify the original user message | Message is displayed correctly |
| 5 | Verify the mid-turn interjection | Message is displayed with "sent while running" label preserved |
| 6 | Verify the agent response | Response is displayed correctly |
| 7 | Verify message sequence | All messages in correct chronological order |

## Expected Final State

After page reload, conversation history displays all messages including mid-turn interjection with correct labels and sequence preserved.

## Pass/Fail Criteria

**Pass:**
- All messages persist after reload
- "Sent while running" label is preserved
- Message sequence is correct

**Fail:**
- Mid-turn message is lost after reload
- Label disappears after reload
- Message order changes after reload
