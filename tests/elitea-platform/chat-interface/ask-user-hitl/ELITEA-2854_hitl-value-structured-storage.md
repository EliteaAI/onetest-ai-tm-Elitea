---
id: ELITEA-2854
title: "ask_user - hitl_value stores structured answers as Dict with only answered questions"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2854: ask_user - hitl_value stores structured answers as Dict with only answered questions

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify hitl_value correctly stores structured answers as Dict[str, Any] with only answered questions.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Developer console or logging access available to inspect tool responses

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Question 1 (text) | Answered: "Test Project" |
| Question 2 (single-select) | Answered: "Option B" |
| Question 3 (multi-select) | Answered: ["Choice1", "Choice3"] |
| Question 4 (text) | Skipped |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable developer tools or logging to inspect tool responses | Console/logs accessible |
| 2 | Trigger ask_user with mixed question types | Clarifying question card appears |
| 3 | Answer question 1 with "Test Project" | Answer recorded |
| 4 | Answer question 2 by selecting "Option B" | Selection recorded |
| 5 | Answer question 3 by selecting "Choice1" and "Choice3" | Multiple selections recorded |
| 6 | Skip question 4 | Question skipped |
| 7 | Submit answers | Card closes |
| 8 | Inspect tool response in console/logs | Tool response visible |
| 9 | Verify hitl_value is a dictionary (Dict[str, Any]) | Structure is dict/object |
| 10 | Verify hitl_value contains question 1: "Test Project" | Key-value pair present |
| 11 | Verify hitl_value contains question 2: "Option B" | Key-value pair present |
| 12 | Verify hitl_value contains question 3: ["Choice1", "Choice3"] | Array value present |
| 13 | Verify hitl_value does NOT contain question 4 | Skipped question not in dict |
| 14 | Verify data types are preserved (string, array, etc.) | Types are correct |

## Expected Final State

hitl_value is a properly structured Dict[str, Any] containing only answered questions with correct data types.

## Pass/Fail Criteria

**Pass:** hitl_value is Dict[str, Any], contains only answered questions, data types preserved, skipped questions excluded

**Fail:** Wrong data structure, includes skipped questions, data types incorrect, missing answered questions
