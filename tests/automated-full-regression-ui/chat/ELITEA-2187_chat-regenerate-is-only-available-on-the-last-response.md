---
id: ELITEA-2187
title: "Chat – Regenerate Is Only Available on the Last Response Not on Earlier Messages"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id:
  - tests.ui.chat.test_chat_regenerate_last_response_only.TestChatRegenerateLastResponseOnly.test_regenerate_only_on_last_of_three_responses
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/586d71d3
---

# ELITEA-2187: Chat – Regenerate Is Only Available on the Last Response Not on Earlier Messages

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that Regenerate appears only on the last response and not on any earlier messages.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least 3 message-response pairs exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Hover over any earlier LLM response (not the last) | No Regenerate text button visible |
| 2 | Hover over the last LLM response | Regenerate button and regenerate icon visible |
| 3 | Click Regenerate on last response | New generation triggered correctly |

---

## Expected Final State

Regenerate is exclusive to the last response.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Regenerate only on last response.

**Fail:**
- Any step produces an error or unexpected result.
- Regenerate on non-last responses.
