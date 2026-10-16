---
id: ELITEA-3968
title: "Clarifying question control supports single-select, multi-select, and free-text answers including an Other option"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, ask-user, clarifying-question-ui]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3968: Clarifying question control supports single-select, multi-select, and free-text answers including an Other option

## Preconditions

- User is logged in to `{{base_url}}`
- Skills Builder and Ask User are enabled

## Test Data

| Field | Value |
|-------|-------|
| Question 1 (single-select) | "Who is the intended audience?" with options Product Managers / Developers / QA Engineers / Other |
| Question 2 (multi-select) | "Which topics should this Skill cover?" with several checkable options |
| Question 3 (free-text) | "What should this Skill help the user accomplish?" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger a clarification flow that includes one single-select, one multi-select, and one free-text question | All three question types render correctly with their respective input controls |
| 2 | On the single-select question, choose "Other" and type a custom value | The custom value is accepted as the answer for that question |
| 3 | On the multi-select question, choose two or more options | Multiple selections are retained simultaneously |
| 4 | On the free-text question, enter a description | Free-text input is accepted |
| 5 | Submit the flow | All three answers, including the custom Other value and the multiple selections, are passed as structured input to the resumed Skill creation |

## Expected Final State

All supported clarifying-question answer types, including the Other free-text option, are captured and used correctly.

## Pass/Fail Criteria

**Pass:**
- All three question types render and accept input correctly
- Other free-text value is accepted and used
- Multi-select retains multiple choices

**Fail:**
- Any question type fails to render or accept input
- Other value or multi-select choices are lost or not passed through
