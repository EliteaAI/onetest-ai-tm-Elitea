---
id: ELITEA-2850
title: "ask_user - Back navigation preserves previously answered questions"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2850: ask_user - Back navigation preserves previously answered questions

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify Back navigation preserves previously answered questions without data loss.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with multiple questions (3+)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Question 1 answer | "Project Alpha" |
| Question 2 answer | "Engineering" |
| Question 3 answer | "$100,000" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger ask_user with multiple questions | Clarifying question card appears |
| 2 | Answer question 1 with "Project Alpha" | Answer recorded |
| 3 | Click Next to move to question 2 | Question 2 appears |
| 4 | Answer question 2 with "Engineering" | Answer recorded |
| 5 | Click Next to move to question 3 | Question 3 appears |
| 6 | Answer question 3 with "$100,000" | Answer recorded |
| 7 | Click Back to return to question 2 | Question 2 appears |
| 8 | Verify answer "Engineering" is still present | Answer is preserved |
| 9 | Click Back to return to question 1 | Question 1 appears |
| 10 | Verify answer "Project Alpha" is still present | Answer is preserved |
| 11 | Navigate forward to question 3 | Question 3 appears |
| 12 | Verify answer "$100,000" is still present | Answer is preserved |
| 13 | Submit all questions | Card closes |
| 14 | Verify agent response uses all three preserved values | Agent uses Project Alpha, Engineering, $100,000 |

## Expected Final State

All answers are preserved during Back/Next navigation without any data loss.

## Pass/Fail Criteria

**Pass:** All answers preserved during navigation, no data loss, agent receives all correct values

**Fail:** Answers lost during navigation, data corruption, agent receives incorrect or missing values
