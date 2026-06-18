---
id: ELITEA-0944
title: "Project Context Is Injected Correctly for Multiple LLM Models"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [project-context, feat:settings, story:3395, r-2.0.4, agents, llm]
requirements: [EliteaAI/elitea_issues#3395]
---
# ELITEA-0944: Project Context Is Injected Correctly for Multiple LLM Models

**Module:** Project Context · **Priority:** High · **Type:** Functional

**Objective:** Verify that Project Context is correctly injected for different LLM models and that switching models does not lose the context.

**Coverage:**
- Context injected for GPT-5-mini
- Context injected for Claude Sonnet
- Context not lost on model switch

## Preconditions

- Logged in to ELITEA (`{{base_url}}`)

## Test Data

- Project Context phrase: `QA-TEST-PHRASE: The gold tide turns at sunrise`
- Models to test: GPT-5-mini, Claude Sonnet (and any other available models)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set Project Context to 'QA-TEST-PHRASE: The gold tide turns at sunrise'. Toggle = ON. Save. | Content and toggle saved. |
| 2 | Open an agent configured with GPT-5-mini on the Agent page. Ask: 'What is the QA-TEST-PHRASE?' | Returns: 'The gold tide turns at sunrise'. |
| 3 | Switch the agent model to Claude Sonnet. Ask the same question. | Claude Sonnet also returns the phrase. |
| 4 | Switch model mid-conversation and ask again. | Context is not lost after model switch — phrase still returned correctly. |

## Expected Final State

Context is not lost after model switch — phrase still returned correctly.

## Pass/Fail Criteria

**Pass:**
- All tested LLM models return the phrase
- Context persists after model switch

**Fail:**
- Any model does not return the phrase with toggle ON
- Context lost after switching models
