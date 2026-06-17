---
id: ELITEA-0224
title: "Selecting a Different LLM Model Updates Chat Toolbar Immediately"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0224: Selecting a Different LLM Model Updates Chat Toolbar Immediately

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that selecting a model from the dropdown updates the displayed model name in the chat toolbar immediately and shows a checkmark on the selected item.

**Coverage:**
- Model selection updates toolbar label in real time
- Selected model is visually marked in the dropdown

## Preconditions

- Published agent is open in chat
- Default model is "Anthropic Claude 4.5 Sonnet"

## Test Data

Switch from Anthropic Claude 4.5 Sonnet to GPT-5.2

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open model dropdown for a published agent. | Dropdown shows available models with current model checked. |
| 2 | Select GPT-5.2 from the list. | Selection is registered. |
| 3 | Observe the chat toolbar model name button. | Button now displays GPT-5.2. |
| 4 | Reopen the dropdown. | GPT-5.2 has a checkmark; Anthropic Claude 4.5 Sonnet does not. |

## Expected Final State

GPT-5.2 has a checkmark; Anthropic Claude 4.5 Sonnet does not.

## Pass/Fail Criteria

**Pass:**
- Toolbar label updates to the selected model name immediately
- Checkmark appears on the newly selected model in the dropdown

**Fail:**
- Toolbar still shows the old model name after selection
- No visual confirmation of selection in dropdown
