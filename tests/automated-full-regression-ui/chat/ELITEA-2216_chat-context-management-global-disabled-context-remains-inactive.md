---
id: ELITEA-2216
title: "Context Management – Global Setting Disabled – Verify Context Management Remains Inactive Regardless of Token Usage"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_context_management_disabled.TestContextManagementDisabledWidgetStaysZero.test_context_management_disabled_widget_stays_at_zero"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1608
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2216: Context Management – Global Setting Disabled – Verify Context Management Remains Inactive Regardless of Token Usage

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that with global context management disabled, the Context Budget widget always shows 0 tokens regardless of conversation length.

---

## Preconditions

- User is logged in to the Elitea platform.
- Context management is DISABLED in Settings > Personalization.

---

## Test Data

| Field | Value |
|-------|-------|
| Messages to send | 5-10 messages | Message example | Hello, please tell me a long story |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Navigate to Settings > user profile > Personalization | Personalization page opens |
| 2 | Verify 'Enable context management for new conversations' toggle is OFF | Toggle is OFF |
| 3 | Navigate to Chats and create a new conversation | Conversation opens |
| 4 | Verify Context Budget widget shows '0 / 64000 tokens', '0%', Messages: 0, Summaries: 0 | Widget shows all zeros |
| 5 | Send 5-10 messages requesting detailed responses | Messages sent; LLM responds |
| 6 | Verify Context Budget widget stays at '0 / 64000 tokens', '0%', Messages: 0, Summaries: 0 | Widget unchanged |
| 7 | Click edit icon on Context Budget widget | Modal opens showing 0 values for all metrics |

---

## Expected Final State

Context management disabled; widget always shows 0.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Widget shows 0 throughout when global setting is off.

**Fail:**
- Any step produces an error or unexpected result.
- Widget shows non-zero values when disabled.
