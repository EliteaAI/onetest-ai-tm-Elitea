---
id: ELITEA-2843
title: "ask_user - Skip button available and moves to next question"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2843: ask_user - Skip button available and moves to next question

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Skip button is available on each question and clicking Skip moves to next question without answering.

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
| 2 | Verify Skip button is visible on first question | Skip button is present |
| 3 | Click Skip button without answering | Move to question 2 without error |
| 4 | Verify question 1 remains unanswered | No answer recorded for question 1 |
| 5 | Answer question 2 | Answer is recorded |
| 6 | Click Next to move to question 3 | Question 3 appears |
| 7 | Click Skip on question 3 | Move past question 3 |
| 8 | Navigate Back to question 1 | Question 1 appears, still unanswered |
| 9 | Verify Skip button is available on all questions | Skip button present on each step |

## Expected Final State

Skip button functions correctly, allows skipping questions without answers, skipped questions remain unanswered.

## Pass/Fail Criteria

**Pass:** Skip button visible on all questions, skipping works without errors, skipped questions remain unanswered

**Fail:** Skip button missing, skip functionality broken, questions marked as answered when skipped
