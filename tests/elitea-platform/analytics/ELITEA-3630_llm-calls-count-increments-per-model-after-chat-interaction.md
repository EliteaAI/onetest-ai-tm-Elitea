---
id: ELITEA-3630
title: "Analytics — LLM Calls Count Increments Per Model After Chat Interaction"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, llm-counting, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6574]
---
# ELITEA-3630: Analytics — LLM Calls Count Increments Per Model After Chat Interaction

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that LLM calls are counted accurately per model when a user sends chat messages using different LLM models.

**Coverage:**
- LLM CALLS KPI increments after each LLM interaction
- Model Usage Breakdown table shows correct CALLS/RUNS per model
- SHARE % is calculated correctly (model calls / total calls × 100)

## Preconditions

- Logged in to {{base_url}}
- User has access to at least 2 different LLM models (e.g., Anthropic Claude 4.6 Sonnet, GPT-5 mini)
- User has access to Settings > Analytics page

## Test Data

| Field | Value |
|-------|-------|
| Model 1 | Anthropic Claude 4.6 Sonnet |
| Model 2 | GPT-5 mini |
| Chat Message | "Hello, what is 2+2?" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Analytics > Overview tab | Analytics page loads. Note current LLM CALLS KPI value (e.g., N) |
| 2 | Navigate to Chats. Create a new chat using Model 1 (Claude 4.6 Sonnet) | Chat created with selected model |
| 3 | Send a simple message: "Hello, what is 2+2?" | LLM responds successfully |
| 4 | Navigate to Settings > Analytics > Overview tab. Check LLM CALLS KPI | LLM CALLS = N + 1 |
| 5 | Scroll to "Model Usage Breakdown" table | Anthropic Claude 4.6 Sonnet row shows incremented CALLS/RUNS count |
| 6 | Navigate to Chats. Create a new chat using Model 2 (GPT-5 mini) | Chat created with selected model |
| 7 | Send the same message: "Hello, what is 2+2?" | LLM responds successfully |
| 8 | Navigate to Settings > Analytics > Overview tab. Check LLM CALLS KPI | LLM CALLS = N + 2 |
| 9 | Verify Model Usage Breakdown shows both models with correct counts | Both models show accurate CALLS/RUNS. SHARE % sums to 100% |

## Expected Final State

LLM CALLS KPI reflects total calls made. Model Usage Breakdown table shows accurate per-model call counts with correct percentage shares.

## Pass/Fail Criteria

**Pass:**
- LLM CALLS KPI increments by 1 for each LLM interaction
- Each model's CALLS/RUNS count is accurate
- SHARE % = (model calls / total calls) × 100

**Fail:**
- LLM CALLS does not increment after interaction
- Model calls are attributed to wrong model
- SHARE % does not sum to 100%
