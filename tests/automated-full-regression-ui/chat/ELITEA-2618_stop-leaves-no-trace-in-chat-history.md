---
id: ELITEA-2618
title: "Chat – No Trace Left in Chat History After Stop"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2618: Chat – No Trace Left in Chat History After Stop

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that after stopping a generation during the thinking phase, the conversation looks exactly as if the message was never sent — no user message bubble and no partial/empty assistant bubble remain, including after a page refresh.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation with at least one prior, completed message exchange (so the conversation is not empty and truncation/deletion is easy to visually verify).

---

## Test Data

| Field | Value |
|-------|-------|
| Message | "stop-trace-test message" |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Note the current last message in the conversation history | Baseline recorded |
| 2 | Send the test message and click Stop while sub-agent/thinking steps are running | Execution stops |
| 3 | Verify the user's message bubble for the stopped prompt is not present in the chat | No user bubble for the stopped message |
| 4 | Verify no empty/partial assistant message bubble is present either | No assistant bubble for the stopped response |
| 5 | Verify the last visible message in the conversation is still the baseline message from step 1 | Chat looks unchanged from before the stopped attempt |
| 6 | Refresh the page / reopen the conversation from the sidebar | Conversation reloads |
| 7 | Verify the stopped message pair is still absent after reload | No trace of the stopped exchange persists server-side |

---

## Expected Final State

The conversation history is identical to its state before the stopped message was sent — no orphaned messages exist locally or persisted server-side.

---

## Pass/Fail Criteria

**Pass:**
- No user or assistant bubble for the stopped exchange appears in the UI.
- After refresh/reopen, the stopped exchange is still absent.

**Fail:**
- Any partial/empty message bubble remains visible.
- The stopped exchange reappears after refresh (indicates it was persisted server-side despite being stopped).
