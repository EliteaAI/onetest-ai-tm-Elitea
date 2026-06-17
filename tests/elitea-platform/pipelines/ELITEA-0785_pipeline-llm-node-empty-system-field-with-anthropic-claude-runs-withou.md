---
id: ELITEA-0785
title: "Pipeline LLM Node: Empty System Field with Anthropic Claude Runs Without Error [Parametrized]"
priority: critical
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, rca:regression, int:litellm, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5163]
---
# ELITEA-0785: Pipeline LLM Node: Empty System Field with Anthropic Claude Runs Without Error [Parametrized]

**Module:** Pipelines · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a pipeline LLM Node configured with an empty system field and an Anthropic Claude model runs successfully without a 400 error.

**Coverage:**
- Pipeline with LLM Node using Anthropic Claude 4.5 Sonnet runs with empty system field
- Pipeline with LLM Node using Anthropic Claude 4.6 Sonnet runs with empty system field
- No `cache_control cannot be set for empty text blocks` error appears
- Pipeline output is returned successfully

## Preconditions

- Logged in to {{base_url}}
- A pipeline with an LLM Node exists (or can be created)
- Anthropic Claude 4.5 Sonnet and/or Claude 4.6 Sonnet is available as a model option

## Test Data

| Variant | Model | System field type | System field value |
|---|---|---|---|
| A | Anthropic Claude 4.5 Sonnet | Fixed | `''` (empty string) |
| B | Anthropic Claude 4.6 Sonnet | Fixed | `''` (empty string) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open or create a pipeline with an LLM Node. Set the model to Anthropic Claude 4.5 Sonnet (Variant A) or 4.6 Sonnet (Variant B). | LLM Node is configured with the selected Anthropic model. |
| 2 | Set the system field to type 'fixed' with an empty value (''). Save the pipeline. | Pipeline is saved successfully. |
| 3 | Run the pipeline with a sample input message. | Pipeline execution starts without immediate error. |
| 4 | Observe the pipeline run result and status. | Pipeline completes successfully. Output is returned. No 400 error and no 'cache_control cannot be set for empty text blocks' error appears. |
| 5 | Repeat steps 1–4 for the other Claude model variant. | Behavior is consistent for both Claude 4.5 and 4.6 Sonnet. |

## Expected Final State

Behavior is consistent for both Claude 4.5 and 4.6 Sonnet.

## Pass/Fail Criteria

**Pass:**
- Pipeline runs successfully with an empty system field on Anthropic Claude models
- No 400 error is returned
- No `cache_control cannot be set for empty text blocks` error appears

**Fail:**
- Pipeline fails with a 400 error
- `cache_control cannot be set for empty text blocks` error appears in the output
- Pipeline run status shows error/failed
