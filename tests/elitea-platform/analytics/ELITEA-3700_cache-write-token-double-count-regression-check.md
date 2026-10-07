---
id: ELITEA-3700
title: "Verify Cache-Write Tokens Are Not Double-Counted for Caching-Capable Models"
priority: critical
type: regression
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, r-2.0.7, bug-env:dev, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6705]
---

# ELITEA-3700: Verify Cache-Write Tokens Are Not Double-Counted for Caching-Capable Models

**Module:** Analytics · **Priority:** Critical · **Type:** Regression

**Objective:** Verify the fixed defect (double-counting `cache_creation_tokens` into billable input for Claude-family calls routed through LiteLLM's `chat/completions` relay) does not regress.

**Coverage:**
- Analytics Input Token cost/count excludes cache-creation tokens
- Analytics Cache Write cost/tokens match LiteLLM's cache-creation figures

## Preconditions

- Admin/owner access to a DEV project (e.g. project 564) with Settings > Analytics and Settings > Usage
- Access to the project's LiteLLM logs for the same window (request-id level)
- A platform-managed caching-capable model (e.g. a Claude-backed Bedrock-GPT-5.6-* model) available as a chat participant

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Model | Bedrock-GPT-5.6-Luna (or equivalent Claude-backed caching-capable model) |
| First message | A long cacheable prompt (≥1024 tokens) followed by "Summarize the above in one sentence." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a new Chat with the caching-capable model as the only participant | Chat created |
| 2 | Send the first message | Model responds; a cache write is triggered |
| 3 | Note the response's request id (chatcmpl-*) | Request id captured |
| 4 | Open the matching LiteLLM log entry for that request id | Record `prompt_tokens`, `cache_creation_tokens`, and computed cost |
| 5 | Open Settings > Analytics > Costs and > Tokens for the same window | Input Token Cost/Tokens and Cache Write Cost/Tokens visible |
| 6 | Compare Analytics Input Tokens/Cost against LiteLLM `prompt_tokens` minus `cache_creation_tokens` | Analytics equals the non-inclusive figure, not the full prompt_tokens |
| 7 | Compare Analytics Cache Write Tokens/Cost against LiteLLM `cache_creation_tokens` and its cost | Figures match within rounding |

## Expected Final State

Analytics' Input Token and Cache Write figures for the test call reconcile exactly with LiteLLM's non-overlapping prompt/cache-creation token breakdown; no double-counting of cache-creation tokens into billable input.

## Pass/Fail Criteria

**Pass:**
- Analytics input tokens/cost = LiteLLM `prompt_tokens` − `cache_creation_tokens` (within rounding)
- Analytics cache-write tokens/cost matches LiteLLM `cache_creation_tokens` and its cost

**Fail:**
- Analytics input tokens/cost includes the full inclusive `prompt_tokens` (cache-creation tokens counted twice)
- Cache Write tokens/cost is zero or missing despite a cache write occurring in LiteLLM
