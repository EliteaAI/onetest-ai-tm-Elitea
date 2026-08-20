---
id: ELITEA-2217
title: "Context Management – Global Setting Enabled, Auto-Summarization Disabled – Verify No Summarization Occurs When Tokens Exceed Max Limit"
priority: medium
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id: "tests.ui.chat.test_context_auto_summarization_disabled.TestContextAutoSummarizationDisabled.test_no_summarization_when_auto_summarization_disabled"
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1608
tags: [automated:UI:regression, feat:chat]
requirements: []
---

# ELITEA-2217: Context Management – Global Setting Enabled, Auto-Summarization Disabled – Verify No Summarization Occurs When Tokens Exceed Max Limit

**Module:** chat-interface · **Priority:** medium · **Type:** functional

**Objective:** Verify that with context management ON but auto-summarization OFF, token count increases but no summarization occurs even when exceeding the max.

---

## Preconditions

- User is logged in to the Elitea platform.
- Context management ON, auto-summarization OFF in Settings.

---

## Test Data

| Field | Value |
|-------|-------|
| Max tokens | 64000 |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Enable 'Enable context management for new conversations', disable 'Enable automatic summarization' in Settings | Settings configured |
| 2 | Create a new conversation | Context Budget shows '0 / 64000', Messages: 0, Summaries: 0 |
| 3 | Send messages until token count exceeds max (>64000) | Token count increases; percentage exceeds 100%; warning icon appears |
| 4 | Verify Summaries count remains at 0 throughout | Summaries always 0 |
| 5 | Verify no 'Summarizing the chat history' indicator appears | No summarization indicator |
| 6 | Open Context Management modal; verify Summaries shows 0; auto-summarization toggle is OFF | Modal confirms no summarization |

---

## Expected Final State

Token usage tracked but no summarization without auto-summarization.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Token count increases; Summaries stays 0.

**Fail:**
- Any step produces an error or unexpected result.
- Summarization occurs when auto-summarization is off.
