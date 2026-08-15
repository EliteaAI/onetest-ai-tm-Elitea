---
id: ELITEA-2114
title: "Chat – Conversation Deletion"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id: tests.ui.chat.test_conversation_deletion_flow.TestConversationDeletionFlow.test_conversation_deletion_cancel_then_delete_active_conversation
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/696
---

# ELITEA-2114: Chat – Conversation Deletion

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that the conversation deletion flow works correctly including the confirmation modal, Cancel preserves the conversation, and Delete removes it from the list.

**Also satisfies:** ELITEA-2456 (Chat – Conversation deletion with cancel and confirm flow) — a
Rule-6 already-covered dedup, 2026-08-15; ELITEA-2456's 13 steps are a strict subset of this
test's own steps. See `test-specs/chat-interface/lcovered_conversation-deletion-cancel-confirm-flow_ELITEA-2456.md`.

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one conversation exists in the Chats section.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Chats and verify conversations list is displayed grouped by date | Conversations listed under Today, This Week, Older |
| 2 | Hover over any conversation and verify three-dot icon appears | Three-dot icon is visible |
| 3 | Click the three-dot icon and verify context menu shows: Rename, Move to, Playback, Make public (project-dependent), Share (project-dependent), Pin on top/Unpin, Delete | Context menu visible |
| 4 | Click Delete | Confirmation modal appears: "Delete confirmation" |
| 5 | Verify modal body reads "Are you sure to delete the <conversation name> chat? It can't be restored." | Modal text is correct |
| 6 | Verify modal has Cancel (secondary) and Delete (red/primary) buttons | Both buttons visible |
| 7 | Click the Cancel button | Modal closes; conversation remains in the list |
| 8 | Hover over the same conversation, open context menu, click Delete again | Confirmation modal appears again |
| 9 | Click the Delete button | Modal closes |
| 10 | Verify the conversation is no longer in the left panel | Conversation removed |
| 11 | Verify no error message appears and next conversation is highlighted | No errors; next conversation is selected |
| 12 | Verify the main chat panel does not show the deleted conversation | Deleted content gone |

---

## Expected Final State

The conversation is deleted after confirmation; Cancel preserves it. The panel refreshes correctly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Cancel preserves conversation; Delete removes it.

**Fail:**
- Any step produces an error or unexpected result.
- Conversation persists after Delete, or Cancel deletes it.
