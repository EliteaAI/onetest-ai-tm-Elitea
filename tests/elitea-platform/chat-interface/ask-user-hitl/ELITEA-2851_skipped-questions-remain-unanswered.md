---
id: ELITEA-2851
title: "ask_user - Skipped questions remain unanswered when navigating Back"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2851: ask_user - Skipped questions remain unanswered when navigating Back

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify skipped questions remain unanswered when navigating Back and can be answered later.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with multiple questions (3+)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Question 1 | Skipped |
| Question 2 | Answered: "Value 2" |
| Question 3 | Skipped |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger ask_user with multiple questions | Clarifying question card appears |
| 2 | Click Skip on question 1 without answering | Move to question 2 |
| 3 | Answer question 2 with "Value 2" | Answer recorded |
| 4 | Click Next to move to question 3 | Question 3 appears |
| 5 | Click Skip on question 3 | Move past question 3 |
| 6 | Click Back to return to question 3 | Question 3 appears |
| 7 | Verify question 3 has no answer (blank/empty) | Question is unanswered |
| 8 | Click Back to return to question 2 | Question 2 appears |
| 9 | Verify "Value 2" is still present | Answer is preserved |
| 10 | Click Back to return to question 1 | Question 1 appears |
| 11 | Verify question 1 has no answer (blank/empty) | Question is unanswered |
| 12 | Answer question 1 with "Retroactive Answer" | Answer is now recorded |
| 13 | Navigate forward and submit | Card closes |
| 14 | Verify agent receives question 1 and 2 answers only | Agent has "Retroactive Answer" and "Value 2", question 3 skipped |

## Expected Final State

Skipped questions remain unanswered on Back navigation, can be answered later, agent receives only answered questions.

## Pass/Fail Criteria

**Pass:** Skipped questions remain blank, can be answered after skip, agent receives only answered questions

**Fail:** Skipped questions show placeholder values, cannot be answered after skip, agent receives skipped questions
