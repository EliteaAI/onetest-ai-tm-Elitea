---
id: ELITEA-0227
title: "LLM Model Dropdown Lists Available Models for Published Agent"
priority: critical
type: functional
module: agents-studio
status: draft
execution_type: manual
tags: [feat: agent-publishing, meta:needs_refinement, r-2.0.3, 4644]
requirements: [EliteaAI/elitea_issues#4644]
---
# ELITEA-0227: LLM Model Dropdown Lists Available Models for Published Agent

**Module:** Agents Studio · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the LLM model selector in a published agent chat opens a dropdown showing the full list of available models.

**Coverage:**
- Dropdown opens on click
- All expected models are listed
- Capability icons visible

## Preconditions

- Logged in to {{base_url}}
- Published Agent Studio agent is open in chat (agentId=16)

## Test Data

Expected models: Anthropic Claude 4.5 Sonnet, Anthropic Claude 4.6 Sonnet, Anthropic Claude Haiku 4.5, Azure Claude Sonnet 4.5, GPT-4.1, GPT-4o mini (shared), GPT-5 mini, GPT-5.2, GPT-5.4, GPT-5.4-mini

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a published agent in chat. | Chat interface is displayed with model selector in toolbar. |
| 2 | Click the LLM model name button in the chat input toolbar. | A dropdown/list opens. |
| 3 | Observe the list of models displayed. | Full list of available models is visible with model names and capability icons. |

## Expected Final State

Full list of available models is visible with model names and capability icons.

## Pass/Fail Criteria

**Pass:**
- Dropdown opens without error
- All expected models are present in the list
- Capability icons (image analysis, reasoning) are visible where applicable

**Fail:**
- Dropdown does not open
- Model list is empty or shows only a subset
- An error is displayed on click
