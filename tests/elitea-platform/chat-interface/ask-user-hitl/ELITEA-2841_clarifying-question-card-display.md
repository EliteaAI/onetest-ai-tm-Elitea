---
id: ELITEA-2841
title: "ask_user - Clarifying question card displays when agent triggers tool"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2841: ask_user - Clarifying question card displays when agent triggers tool

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when ask_user tool is enabled and agent triggers it, clarifying question card displays with agent-generated questions.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled in internal tools settings
- User has an active chat conversation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Initial prompt | "Help me plan a vacation" |
| Expected questions | Budget, destination preferences, dates, travelers count, etc. |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send initial prompt that requires clarification | Agent processes the message |
| 2 | Wait for agent to trigger ask_user tool | Agent execution pauses |
| 3 | Observe the chat interface | Clarifying question card appears in chat |
| 4 | Verify card contains agent-generated questions | Questions are displayed clearly |
| 5 | Verify card has clear visual distinction from normal messages | Card has distinct styling (border, background, etc.) |

## Expected Final State

Clarifying question card is displayed with agent-generated questions in a visually distinct format.

## Pass/Fail Criteria

**Pass:** Card appears when agent triggers ask_user, questions are visible and readable, card is visually distinct

**Fail:** Card does not appear, questions are missing or malformed, no visual distinction
