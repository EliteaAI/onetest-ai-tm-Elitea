---
id: ELITEA-0786
title: "Pipeline LLM Node: Non-Empty System Prompt with Anthropic Claude Still Works [Parametrized]"
priority: high
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, rca:regression, int:litellm, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5163]
---
# ELITEA-0786: Pipeline LLM Node: Non-Empty System Prompt with Anthropic Claude Still Works [Parametrized]

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the fix for the empty system field bug did not break the cache_control path for non-empty system prompts on Anthropic Claude models.

**Coverage:**
- LLM Node with non-empty system prompt on Claude 4.5 Sonnet executes correctly
- LLM Node with non-empty system prompt on Claude 4.6 Sonnet executes correctly
- System prompt is applied to the response
- No regression introduced by the truthiness guard fix

## Preconditions

- Logged in to {{base_url}}
- A pipeline with an LLM Node exists using Anthropic Claude 4.5 or 4.6 Sonnet

## Test Data

| Variant | Model | System field value |
|---|---|---|
| A | Anthropic Claude 4.5 Sonnet | `"You are a helpful assistant. Return Response in UPPERCASE"` |
| B | Anthropic Claude 4.6 Sonnet | `"You are a helpful assistant.  Return Response in UPPERCASE"` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline's LLM Node. Set the model to the variant's Anthropic Claude model. Set the system field to a non-empty value (e.g., 'You are a helpful assistant.'). Save. | Node is configured and pipeline is saved. |
| 2 | Set the task. Run the pipeline with a sample input. | Pipeline execution starts. |
| 3 | Observe the run result and output. | Pipeline completes successfully. The system prompt is applied. No errors. |
| 4 | Repeat for the other Anthropic model variant. | Behavior is consistent — cache_control applies correctly for non-empty system prompts on both Anthropic Claude 4.5 and 4.6 Sonnet. |

## Expected Final State

Behavior is consistent — cache_control applies correctly for non-empty system prompts on both Anthropic Claude 4.5 and 4.6 Sonnet.

## Pass/Fail Criteria

**Pass:**
- Pipeline runs successfully with a non-empty system prompt on Anthropic Claude
- System prompt behavior is applied correctly
- No errors or regressions introduced

**Fail:**
- Pipeline fails despite a valid non-empty system prompt
- Fix broke the non-empty system prompt (cache_control) path
