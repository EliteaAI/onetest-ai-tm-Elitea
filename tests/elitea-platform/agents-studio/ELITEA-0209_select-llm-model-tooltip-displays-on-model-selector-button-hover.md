---
id: ELITEA-0209
title: "Select LLM Model Tooltip Displays on Model Selector Button Hover"
priority: medium
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0209: Select LLM Model Tooltip Displays on Model Selector Button Hover

**Module:** Agents Studio · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that hovering over the model selector button in the chat toolbar displays a "Select LLM Model" tooltip (or equivalent).

**Coverage:**
- Tooltip visible on hover
- Tooltip text is correct

## Preconditions

- Published agent is open in chat, chat toolbar is visible

## Test Data

Tooltip expected text: "Select LLM Model" (or similar)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open published agent in chat. | Chat toolbar visible. |
| 2 | Hover the mouse over the LLM model name button in the toolbar without clicking. | Tooltip appears after a brief hover delay. |
| 3 | Read the tooltip text. | Text matches 'Select LLM Model' or an equivalent label. |

## Expected Final State

Text matches 'Select LLM Model' or an equivalent label.

## Pass/Fail Criteria

**Pass:**
- Tooltip appears on hover with correct text

**Fail:**
- No tooltip appears
- Tooltip text is incorrect or empty
