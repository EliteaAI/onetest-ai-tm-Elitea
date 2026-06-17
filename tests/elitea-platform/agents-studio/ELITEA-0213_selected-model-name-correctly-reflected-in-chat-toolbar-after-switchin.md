---
id: ELITEA-0213
title: "Selected Model Name Correctly Reflected in Chat Toolbar After Switching"
priority: high
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0213: Selected Model Name Correctly Reflected in Chat Toolbar After Switching

**Module:** Agents Studio · **Priority:** High · **Type:** Functional

**Objective:** Verify that after switching models, the chat toolbar button always displays the exact name of the currently selected model.

**Coverage:**
- Toolbar label updates correctly after each model switch
- Model name is not truncated or corrupted

## Preconditions

- Published agent is open in chat

## Test Data

Switch sequence: Anthropic Claude 4.5 Sonnet → GPT-5.4-mini → Azure Claude Sonnet 4.5

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Note initial model in toolbar: Anthropic Claude 4.5 Sonnet. | Confirmed. |
| 2 | Open dropdown, select GPT-5.4-mini. | Toolbar shows GPT-5.4-mini. |
| 3 | Open dropdown, select Azure Claude Sonnet 4.5. | Toolbar shows Azure Claude Sonnet 4.5. |

## Expected Final State

Toolbar shows Azure Claude Sonnet 4.5.

## Pass/Fail Criteria

**Pass:**
- Toolbar label matches the selected model name exactly after each switch
- Full model name is readable (not truncated to unrecognizable length)

**Fail:**
- Toolbar shows wrong model name after switch
- Toolbar label is blank, truncated, or shows a stale value
