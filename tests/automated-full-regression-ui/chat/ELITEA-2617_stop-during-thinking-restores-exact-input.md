---
id: ELITEA-2617
title: "Chat – Stop During Thinking Phase Halts Execution and Restores Exact Original Input"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:5196]
requirements: [EliteaAI/elitea_issues#5196]
---

# ELITEA-2617: Chat – Stop During Thinking Phase Halts Execution and Restores Exact Original Input

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Stop while sub-agents are working immediately halts execution, re-enables the input box, and places the exact original question text back into the input field.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has an open conversation with an agent that performs visible thinking/tool-call steps.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | "Please research and summarize the latest 5 open issues, including special chars: café/naïve #test" |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Type the test message and click Send | User message appears; thinking/sub-agent steps begin; Stop button visible |
| 2 | While thinking/sub-agent steps are still running, click Stop | Execution halts immediately (no further thinking steps or content appear) |
| 3 | Verify the input box is re-enabled right away | Input field is editable/focusable immediately after stop |
| 4 | Verify the input box now contains the exact original message text (including special characters), not a placeholder or partial text | Input field shows the identical text that was originally sent |

---

## Expected Final State

Execution is stopped, input is re-enabled, and the exact original question is restored to the input box, ready to resend or edit.

---

## Pass/Fail Criteria

**Pass:**
- Stop halts execution promptly during the thinking phase.
- Input box is immediately editable.
- Restored text exactly matches the original message (character-for-character).

**Fail:**
- Execution continues after Stop is clicked.
- Input remains disabled after stop.
- Restored text differs from the original (missing/altered characters, truncated, or empty).
