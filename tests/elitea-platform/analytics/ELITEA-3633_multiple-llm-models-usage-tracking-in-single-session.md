---
id: ELITEA-3633
title: "Analytics — Multiple LLM Models Usage Tracking in Single Session"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, llm-counting, multi-model, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6574]
---
# ELITEA-3633: Analytics — Multiple LLM Models Usage Tracking in Single Session

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that usage is tracked correctly when a user interacts with multiple different LLM models within a single session.

**Coverage:**
- Each model's usage is tracked separately
- No cross-contamination of metrics between models
- Model Usage Breakdown accurately reflects all models used

## Preconditions

- Logged in to {{base_url}}
- User has access to multiple LLM models (at least 3: Claude, GPT, Bedrock)
- Initial Analytics state is noted

## Test Data

| Field | Value |
|-------|-------|
| Model 1 | Anthropic Claude 4.6 Sonnet |
| Model 2 | GPT-5 mini |
| Model 3 | Bedrock-GPT-5.6-Terra |
| Test Message | "What is AI?" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Analytics > Overview. Note Model Usage Breakdown for all 3 models | Initial counts recorded |
| 2 | Create chat with Model 1 (Claude). Send "What is AI?" | Response received |
| 3 | Create chat with Model 2 (GPT-5). Send "What is AI?" | Response received |
| 4 | Create chat with Model 3 (Bedrock). Send "What is AI?" | Response received |
| 5 | Navigate to Analytics > Overview | LLM CALLS KPI increased by 3 |
| 6 | Check Model Usage Breakdown | Each of the 3 models shows +1 call |
| 7 | Navigate to Tokens tab. Check Token Usage by Model | Each model shows tokens consumed for that interaction only |
| 8 | Navigate to Costs tab. Check Cost by Model | Each model shows cost for that interaction only |

## Expected Final State

Each model's metrics are tracked independently. No metrics from one model appear under another model's row.

## Pass/Fail Criteria

**Pass:**
- Each model shows exactly +1 call
- Token/cost attribution is model-specific
- No cross-contamination between model rows

**Fail:**
- Calls counted under wrong model
- Tokens/costs mixed between models
