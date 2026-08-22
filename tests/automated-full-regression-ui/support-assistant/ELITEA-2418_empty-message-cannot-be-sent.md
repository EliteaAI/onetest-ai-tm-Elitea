---
id: ELITEA-2418
title: "Empty message cannot be sent"
priority: high
type: functional
module: support-assistant
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
automation_test_id: tests.ui.support_assistant.test_support_assistant_empty_message.TestSupportAssistantEmptyMessage.test_empty_message_cannot_be_sent
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1651
---

# ELITEA-2418: Empty message cannot be sent

**Module:** support-assistant · **Priority:** high · **Type:** functional

**Objective:** Verify that Empty message cannot be sent. Success is confirmed when type actual text — verify the send button becomes enabled.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Support Assistant widget | Target page/section loads successfully. |
| 2 | Ensure the message input field is empty (clear any existing text) | Condition holds as described. |
| 3 | Verify the Send button is disabled | Condition holds as described. |
| 4 | Press the Enter key — verify no message is sent and the conversation is unchanged | Control responds; expected next state is shown. |
| 5 | Type a single space character — verify the Send button remains disabled (whitespace-only input not allowed) | Field accepts the input and displays the entered value. |
| 6 | Type actual text — verify the Send button becomes enabled | Field accepts the input and displays the entered value. |

---

## Expected Final State

Type actual text — verify the Send button becomes enabled.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Empty message cannot be sent.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
