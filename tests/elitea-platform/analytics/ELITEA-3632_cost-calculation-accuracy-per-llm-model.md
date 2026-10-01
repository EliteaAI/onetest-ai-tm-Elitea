---
id: ELITEA-3632
title: "Analytics — Cost Calculation Accuracy Per LLM Model"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, costs, llm-counting, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6574]
---
# ELITEA-3632: Analytics — Cost Calculation Accuracy Per LLM Model

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that costs are calculated accurately based on token consumption and model pricing.

**Coverage:**
- Total Cost = Input Token Cost + Output Token Cost + Cache Read Cost + Cache Write Cost
- Cost by Model table shows accurate per-model costs
- Cost by User table attributes costs correctly

## Preconditions

- Logged in to {{base_url}}
- User has made LLM calls
- User has access to Settings > Analytics > Costs tab

## Test Data

| Field | Value |
|-------|-------|
| Model | Anthropic Claude 4.6 Sonnet |
| Expected Cost Components | Input, Output, Cache Read, Cache Write |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Analytics > Costs tab | Costs page loads. Note banner: "Costs are estimated from a local model-price table" |
| 2 | Note TOTAL COST KPI value | Total cost displayed in USD |
| 3 | Note INPUT TOKEN COST, OUTPUT TOKEN COST, CACHE READ COST, CACHE WRITE COST | All cost components displayed |
| 4 | Verify: TOTAL COST = INPUT + OUTPUT + CACHE READ + CACHE WRITE costs | Calculation matches |
| 5 | Check "Cost by Model" table | Each model shows: Total Cost, Input Token Cost, Output Token Cost, Cache Read Cost, Cache Write Cost, Share % |
| 6 | Verify Sum(Cost by Model: Total Cost) ≈ TOTAL COST KPI | Aggregation is accurate |
| 7 | Check "Cost by User" table | Current user shows their share of costs |
| 8 | Verify user's SHARE % = (user cost / total cost) × 100 | Percentage is accurate |

## Expected Final State

Costs are calculated accurately based on token usage and model pricing. Per-model and per-user cost attribution is correct.

## Pass/Fail Criteria

**Pass:**
- Total Cost = sum of cost components
- Per-model costs reflect token usage × model pricing
- User attribution is accurate

**Fail:**
- Cost calculation is incorrect
- Costs attributed to wrong model/user
- Missing cost components
