---
id: ELITEA-2852
title: "ask_user - Partial skip scenario with agent receiving only answered questions"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2852: ask_user - Partial skip scenario with agent receiving only answered questions

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify partial skip scenario where some questions are answered and some skipped, agent receives only answered questions and asks about skipped ones.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with multiple questions (4+)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Question 1 | Answered: "Alpha" |
| Question 2 | Skipped |
| Question 3 | Answered: "Gamma" |
| Question 4 | Skipped |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger ask_user with 4 questions | Clarifying question card appears |
| 2 | Answer question 1 with "Alpha" | Answer recorded |
| 3 | Click Next, then Skip question 2 | Move to question 3 |
| 4 | Answer question 3 with "Gamma" | Answer recorded |
| 5 | Click Next, then Skip question 4 | Card closes |
| 6 | Observe agent response | Agent generates response |
| 7 | Verify agent uses answered values ("Alpha", "Gamma") | Agent references Alpha and Gamma |
| 8 | Verify agent asks about skipped questions (2, 4) in natural language | Agent message requests missing information |
| 9 | Respond to agent's follow-up question | Provide missing data |
| 10 | Verify agent continues with complete information | Agent completes task with all data |

## Expected Final State

Agent receives only answered questions, uses them in response, and follows up naturally about skipped questions.

## Pass/Fail Criteria

**Pass:** Agent receives only answered questions, uses them correctly, asks about skipped ones in natural language

**Fail:** Agent receives skipped questions as answered, does not ask about missing data, execution fails
