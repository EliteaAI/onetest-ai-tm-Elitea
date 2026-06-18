---
id: ELITEA-0784
title: "Pipeline with Multiple LLM Nodes (Mixed Empty/Non-Empty System Prompt) Runs Successfully Using Anthropic Claude"
priority: high
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipeline_nodes, feat:pipelines, rca:regression, int:litellm, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5163]
---
# ELITEA-0784: Pipeline with Multiple LLM Nodes (Mixed Empty/Non-Empty System Prompt) Runs Successfully Using Anthropic Claude

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that a pipeline with multiple LLM Nodes — some with non-empty system prompts and some with empty system prompts — executes fully without error when using Anthropic Claude models.

**Coverage:**
- Pipeline with multiple LLM Nodes using Anthropic Claude runs end-to-end
- Nodes with non-empty system prompt complete successfully
- Nodes with empty system prompt complete successfully (fix applied)
- No `cache_control` errors on any node

## Preconditions

- Logged in to {{base_url}}
- A pipeline exists (or is created) with multiple LLM Nodes all using Anthropic Claude 4.5 or 4.6 Sonnet — at least one node has a non-empty system prompt and at least one has an empty system prompt

## Test Data

| LLM Node | Model | System prompt |
|---|---|---|
| Node 1 | Anthropic Claude 4.5 / 4.6 Sonnet | Non-empty (e.g., `"You are a helpful assistant."`) |
| Node 2 | Anthropic Claude 4.5 / 4.6 Sonnet | Empty (`''`) |
| Node 3+ (optional) | Anthropic Claude 4.5 / 4.6 Sonnet | Any |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline. Confirm at least one LLM Node has a non-empty system prompt and at least one has an empty system prompt. All nodes use Anthropic Claude 4.5 or 4.6 Sonnet. | Pipeline structure is confirmed. |
| 2 | Run the pipeline with a sample input. | Pipeline execution starts. All LLM Nodes are processed in sequence. |
| 3 | Observe the overall pipeline run status. | Pipeline completes successfully. No 400 error or `cache_control cannot be set for empty text blocks` error appears. |
| 4 | Check run details or logs for each LLM Node. | Each node has a populated result. No errors in any node-level output. |

## Expected Final State

Each node has a populated result. No errors in any node-level output.

## Pass/Fail Criteria

**Pass:**
- All LLM Nodes complete successfully regardless of empty or non-empty system prompt
- No `cache_control` or 400 errors on any node
- Pipeline run status is successful

**Fail:**
- Any LLM Node fails with 400 error
- Empty-system node still triggers `cache_control cannot be set for empty text blocks`
- Pipeline run status shows failed/error
