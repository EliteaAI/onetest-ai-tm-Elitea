---
id: ELITEA-3668
title: "Analytics — Image Generation Call and Token Counting"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, image-generation, llm-counting, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6571]
---
# ELITEA-3668: Analytics — Image Generation Call and Token Counting

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that generating an image via chat is counted correctly in Analytics — the LLM Calls KPI increments, and the image-generation model shows the call with reasonable input/output token counts.

**Coverage:**
- LLM CALLS KPI increments after an image-generation call
- Model Usage Breakdown table shows the image-generation model's CALLS/RUNS incremented
- Token Usage by Model shows non-zero, reasonable input/output tokens for the call

## Preconditions

- Logged in to {{base_url}}
- Access to the image-generation tool in chat
- Access to Settings > Analytics

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Generate an image of a red bicycle on a white background" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Analytics > Overview tab | Note current LLM CALLS KPI value (e.g., N) |
| 2 | Navigate to Chats. Generate an image using the test prompt | Image is generated and returned successfully |
| 3 | Navigate to Settings > Analytics > Overview tab | LLM CALLS = N + 1 |
| 4 | Scroll to "Model Usage Breakdown" table | The image-generation model's row shows CALLS/RUNS incremented by 1 |
| 5 | Navigate to Analytics > Tokens tab. Check the model's INPUT/OUTPUT TOKENS | Both are non-zero and look reasonable for the prompt sent and the image returned |

## Expected Final State

LLM CALLS KPI and Model Usage Breakdown reflect the image-generation call, with non-zero input/output tokens recorded for the model.

## Pass/Fail Criteria

**Pass:**
- LLM CALLS increments by 1
- Image-generation model shows the call with non-zero, reasonable input/output tokens

**Fail:**
- LLM CALLS does not increment
- Tokens are 0, missing, or clearly unreasonable for the call made
