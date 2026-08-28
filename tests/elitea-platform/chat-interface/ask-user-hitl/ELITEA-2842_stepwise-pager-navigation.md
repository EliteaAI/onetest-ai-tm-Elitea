---
id: ELITEA-2842
title: "ask_user - Stepwise pager with Back/Next navigation and answer validation"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2842: ask_user - Stepwise pager with Back/Next navigation and answer validation

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify stepwise pager displays one question per step, Back/Next navigation works, and Next is disabled until current question is answered.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with multiple questions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Question count | 3+ questions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger ask_user tool with multiple questions | Clarifying question card appears |
| 2 | Verify only the first question is visible | Only question 1 is shown |
| 3 | Verify Back button is disabled on first question | Back button is disabled or hidden |
| 4 | Verify Next button is disabled without answer | Next button is disabled |
| 5 | Answer the first question | Answer is recorded |
| 6 | Verify Next button becomes enabled | Next button is now enabled |
| 7 | Click Next button | Question 2 appears, question 1 is hidden |
| 8 | Click Back button | Question 1 reappears with previous answer preserved |
| 9 | Navigate forward through all questions | Each question displays one at a time |
| 10 | Verify progress indicator shows current step | Step indicator shows "2 of 3", etc. |

## Expected Final State

Pager navigation works correctly, only one question visible at a time, Next disabled until answered, Back preserves answers.

## Pass/Fail Criteria

**Pass:** One question per step, Back/Next work correctly, Next disabled without answer, answers preserved on navigation

**Fail:** Multiple questions visible, navigation broken, Next enabled without answer, answers lost
