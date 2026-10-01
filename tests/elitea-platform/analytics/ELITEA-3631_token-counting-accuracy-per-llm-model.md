---
id: ELITEA-3631
title: "Analytics — Token Counting Accuracy Per LLM Model"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, tokens, llm-counting, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6574]
---
# ELITEA-3631: Analytics — Token Counting Accuracy Per LLM Model

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that token consumption (input, output, cache read, cache write) is tracked accurately per LLM model.

**Coverage:**
- Total Tokens = Input Tokens + Output Tokens
- Token Usage by Model table shows accurate breakdown
- Cache Read and Cache Write tokens are tracked separately

## Preconditions

- Logged in to {{base_url}}
- User has made LLM calls using multiple models
- User has access to Settings > Analytics > Tokens tab

## Test Data

| Field | Value |
|-------|-------|
| Test Prompt | "Explain the theory of relativity in 100 words" |
| Expected Token Range | Input: 10-20, Output: 80-150 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Analytics > Tokens tab | Tokens page loads. Note current TOTAL TOKENS value |
| 2 | Note INPUT TOKENS, OUTPUT TOKENS, CACHE READ, CACHE WRITE KPI values | All KPI values displayed |
| 3 | Verify: TOTAL TOKENS ≈ INPUT TOKENS + OUTPUT TOKENS | Calculation is accurate (cache tokens may add to total) |
| 4 | Navigate to Chats. Send a prompt that generates substantial output | LLM responds with ~100 word response |
| 5 | Return to Analytics > Tokens tab | Token counts have increased |
| 6 | Check "Token Usage by Model" table | Model used shows increased tokens in correct columns |
| 7 | Verify token breakdown: INPUT TOKENS, OUTPUT TOKENS for the model | Input tokens ≈ prompt length, Output tokens ≈ response length |
| 8 | Verify Sum(Token Usage by Model: Total Tokens) = TOTAL TOKENS KPI | Aggregation is accurate |

## Expected Final State

Token counts accurately reflect LLM usage. Per-model breakdown matches total KPIs. Input/output token ratio is reasonable for the conversation.

## Pass/Fail Criteria

**Pass:**
- Token counts increment after LLM interaction
- Per-model token attribution is accurate
- Total = Sum of model breakdowns

**Fail:**
- Tokens not counted
- Tokens attributed to wrong model
- Math discrepancy between totals and breakdowns
