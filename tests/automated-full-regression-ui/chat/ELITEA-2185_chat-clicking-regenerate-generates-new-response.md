---
id: ELITEA-2185
title: "Chat – Clicking Regenerate Generates a New Response Based on Previous User Input"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:chat]
requirements: []
automation_test_id:
  - tests.ui.chat.test_chat_regenerate_new_response.TestChatRegenerateNewResponse.test_regenerate_creates_new_response_same_user_input
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/f8589df5
---

# ELITEA-2185: Chat – Clicking Regenerate Generates a New Response Based on Previous User Input

**Module:** chat-interface · **Priority:** high · **Type:** functional

**Objective:** Verify that clicking Regenerate replaces the current response with a new one based on the previous user message.

---

## Preconditions

- User is logged in to the Elitea platform.
- A conversation with at least one user message and LLM response exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Scroll to last LLM response and hover over it | Regenerate button visible |
| 2 | Click the Regenerate button (circular arrows icon) | Previous response replaced; new generation begins |
| 3 | Verify model label and spinning loading circle on new response | Loading indicator visible |
| 4 | Verify user's previous input remains unchanged | User message unchanged |
| 5 | Verify new response streams and completes | Full response generated |
| 6 | Verify Regenerate and action icons reappear after completion | Actions visible again |

---

## Expected Final State

New response generated; previous user message unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Regenerate generates new response; user message unchanged.

**Fail:**
- Any step produces an error or unexpected result.
- Regenerate fails or user message changed.
