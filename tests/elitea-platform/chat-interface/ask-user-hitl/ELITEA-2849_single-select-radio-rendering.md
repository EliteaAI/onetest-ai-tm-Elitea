---
id: ELITEA-2849
title: "ask_user - Single-select questions render as radio buttons with value captured"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2849: ask_user - Single-select questions render as radio buttons with value captured

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify single-select questions render as radio buttons and selected value is captured correctly.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with single-select questions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Question | "What is your experience level?" |
| Options | Beginner, Intermediate, Advanced, Expert |
| Selected value | Intermediate |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger ask_user with single-select question | Clarifying question card appears |
| 2 | Verify options are rendered as radio buttons | Radio buttons visible for each option |
| 3 | Select "Beginner" radio button | Beginner is selected |
| 4 | Select "Intermediate" radio button | Intermediate selected, Beginner deselected |
| 5 | Verify only one option can be selected at a time | Intermediate is only selected option |
| 6 | Verify Next button becomes enabled | Next button is enabled |
| 7 | Navigate to next question and back | Return to single-select question |
| 8 | Verify "Intermediate" selection is preserved | Intermediate remains selected |
| 9 | Change selection to "Advanced" | Advanced selected, Intermediate deselected |
| 10 | Complete and submit all questions | Card closes |
| 11 | Verify agent response uses the final selected value | Agent references "Advanced" level |

## Expected Final State

Single-select questions use radio buttons, only one selection allowed, value is captured and used by agent.

## Pass/Fail Criteria

**Pass:** Radio buttons render correctly, mutual exclusivity works, final value captured and used by agent

**Fail:** Wrong control type, multiple selections allowed, value not captured or incorrect value used
