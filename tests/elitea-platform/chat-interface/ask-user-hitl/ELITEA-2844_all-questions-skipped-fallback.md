---
id: ELITEA-2844
title: "ask_user - All questions skipped closes card and agent asks in natural language"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2844: ask_user - All questions skipped closes card and agent asks in natural language

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when all questions are skipped, card closes and agent asks user about missing data in natural language.

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
| 2 | Click Skip on question 1 | Move to question 2 |
| 3 | Click Skip on question 2 | Move to question 3 |
| 4 | Click Skip on question 3 (final question) | Card closes |
| 5 | Observe agent response | Agent sends natural language message |
| 6 | Verify agent message asks about the missing information | Message requests clarification on skipped items |
| 7 | Respond to agent's natural language question | Agent processes the response |
| 8 | Verify agent continues execution with user's answers | Agent completes task with provided information |

## Expected Final State

Card closes after all skips, agent follows up in natural language to gather missing information.

## Pass/Fail Criteria

**Pass:** Card closes when all skipped, agent asks about missing data in chat, conversation continues naturally

**Fail:** Card remains visible, agent does not follow up, execution fails or hangs
