---
id: ELITEA-3670
title: "Analytics — Image Reading (Vision Input) Call and Token Counting"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, image-reading, llm-counting, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6571]
---
# ELITEA-3670: Analytics — Image Reading (Vision Input) Call and Token Counting

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that uploading an image into a chat message and asking a vision-capable model about it is counted correctly in Analytics, with input tokens reflecting the image, not just the text prompt.

**Coverage:**
- LLM CALLS KPI increments after an image-reading call
- INPUT TOKENS reflect the image, not just the accompanying text
- OUTPUT TOKENS reflect the generated description

## Preconditions

- Logged in to {{base_url}}
- Access to a vision-capable model in chat
- A test image ready to upload

## Test Data

| Field | Value |
|-------|-------|
| Prompt text | "What is shown in this image?" |
| Image | Any test image (e.g. a product photo) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings > Analytics > Overview tab | Note current LLM CALLS KPI value (e.g., N) |
| 2 | Navigate to Chats. Upload the test image and send it with the prompt text, using a vision-capable model | Model responds describing the image |
| 3 | Navigate to Settings > Analytics > Overview tab | LLM CALLS = N + 1 |
| 4 | Navigate to Analytics > Tokens tab. Check the model's INPUT TOKENS for this call | Input tokens are noticeably higher than a plain text message of similar prompt length would produce — confirms the image itself is being counted |
| 5 | Check OUTPUT TOKENS | Non-zero, reasonable for the length of the description returned |

## Expected Final State

The image-reading call is counted in LLM Calls, with input tokens that visibly reflect the image, not just the short text prompt.

## Pass/Fail Criteria

**Pass:**
- LLM CALLS increments by 1
- Input tokens are clearly higher than what the text prompt alone would produce

**Fail:**
- LLM CALLS does not increment
- Input tokens look the same as a text-only message, or are 0/missing
