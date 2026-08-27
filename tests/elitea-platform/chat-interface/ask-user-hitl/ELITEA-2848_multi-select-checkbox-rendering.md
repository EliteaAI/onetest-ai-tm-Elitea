---
id: ELITEA-2848
title: "ask_user - Multi-select questions render as checkboxes with all values captured"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [chat, hitl, internal-tools, ask-user, issue:6095]
requirements: [EliteaAI/elitea_issues#6095]
---

# ELITEA-2848: ask_user - Multi-select questions render as checkboxes with all values captured

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify multi-select questions render as checkboxes and all selected values are captured correctly.

## Preconditions

- User is logged in to `{{base_url}}`
- ask_user tool is enabled
- Agent has triggered ask_user with multi-select questions

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Question | "Select all programming languages you know" |
| Options | Python, JavaScript, Java, C++, Go |
| Selected values | Python, JavaScript, Go |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger ask_user with multi-select question | Clarifying question card appears |
| 2 | Verify options are rendered as checkboxes | Checkboxes visible for each option |
| 3 | Select Python checkbox | Python is checked |
| 4 | Select JavaScript checkbox | JavaScript is checked, Python remains checked |
| 5 | Select Go checkbox | Go is checked, previous selections remain |
| 6 | Uncheck JavaScript checkbox | JavaScript unchecked, Python and Go remain checked |
| 7 | Re-check JavaScript | JavaScript checked again |
| 8 | Verify Next button is enabled with selections | Next button is enabled |
| 9 | Navigate to next question and back | Return to multi-select question |
| 10 | Verify all selections are preserved | Python, JavaScript, Go remain checked |
| 11 | Complete and submit all questions | Card closes |
| 12 | Verify agent response references all selected values | Agent mentions Python, JavaScript, and Go |

## Expected Final State

Multi-select questions use checkboxes, multiple selections work correctly, all values are captured and used by agent.

## Pass/Fail Criteria

**Pass:** Checkboxes render correctly, multiple selections work, all values preserved and used by agent

**Fail:** Wrong control type (radio instead of checkbox), selections lost, not all values captured
