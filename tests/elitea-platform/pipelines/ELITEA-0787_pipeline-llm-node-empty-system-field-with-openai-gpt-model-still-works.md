---
id: ELITEA-0787
title: "Pipeline LLM Node: Empty System Field with OpenAI GPT Model Still Works"
priority: high
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, rca:regression, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5163]
---
# ELITEA-0787: Pipeline LLM Node: Empty System Field with OpenAI GPT Model Still Works

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Anthropic-specific fix did not introduce a regression for OpenAI GPT models — pipelines with an empty system field on GPT models should continue to work as before.

**Coverage:**
- LLM Node with empty system field on an OpenAI GPT model runs successfully
- GPT model behavior is unaffected by the Anthropic cache_control guard fix

## Preconditions

- Logged in to {{base_url}}
- A pipeline with an LLM Node using an OpenAI GPT model (e.g., GPT-4o)

## Test Data

| Field | Value |
|---|---|
| Model | Any OpenAI GPT model (e.g., GPT-4o) |
| System field type | Fixed |
| System field value | `''` (empty string) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline with LLM Nodes. Set the model to an OpenAI GPT model (e.g., GPT-4o). Set the system field to 'fixed' with an empty value (''). Save. | Node is configured and pipeline is saved. |
| 2 | Run the pipeline with a sample input. | Pipeline execution starts. |
| 3 | Observe the run result and output. | Pipeline completes successfully. No errors. GPT model behavior is unaffected by the Anthropic-specific fix. |

## Expected Final State

Pipeline completes successfully. No errors. GPT model behavior is unaffected by the Anthropic-specific fix.

## Pass/Fail Criteria

**Pass:**
- Pipeline runs successfully with empty system field on GPT model
- No regression introduced for non-Anthropic models

**Fail:**
- GPT model pipeline now fails where it previously worked
- Empty system field causes an unexpected error on GPT models
