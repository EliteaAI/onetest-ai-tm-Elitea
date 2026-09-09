---
id: ELITEA-3361
title: "Multi-turn Chat with Image Follow-up Questions"
priority: high
type: integration
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, feat:image-vision, r-2.0.6, feat:chat]
requirements: [EliteaAI/elitea_issues#6530, EliteaAI/elitea_issues#6431]
---
# ELITEA-3361: Multi-turn Chat with Image Follow-up Questions

**Module:** Artifacts Toolkit Read File · **Priority:** High · **Type:** Integration

**Objective:** Verify that in a multi-turn chat, the LLM can ask follow-up questions about a previously read image using `read_file` with custom `user_prompt`.

**Coverage:**
- Multi-turn conversation with images
- Follow-up questions using custom prompts
- Image accessibility in chat history (related to #6431)

## Preconditions

- Logged in to dev environment
- Chat with Artifact Toolkit available
- Multimodal LLM configured
- `infographic.png` in bucket `test` (complex image with multiple data points)

## Test Data

| Turn | Action | Expected |
|---|---|---|
| 1 | Generic read | Overall description |
| 2 | Follow-up with custom prompt | Specific detail answer |
| 3 | Another follow-up | Another specific answer |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In chat, send: "Read infographic.png from bucket test and describe it." | LLM calls `read_file` without custom prompt; returns generic description. |
| 2 | Follow up: "What is the percentage shown in the top-left corner?" | LLM calls `read_file` again with `extra_params={"user_prompt": "What is the percentage in the top-left corner?"}`. |
| 3 | Verify response answers the specific question. | Response: "X%" — the specific percentage, not the generic description. |
| 4 | Ask another follow-up: "And what about the bottom section?" | LLM uses `user_prompt` for this new question. |
| 5 | Verify image remains accessible throughout conversation. | No errors about image not found or inaccessible. |

## Expected Final State

Multi-turn conversation successfully uses different `user_prompt` values for the same image in follow-up questions.

## Pass/Fail Criteria

**Pass:**
- Generic description in first turn
- Specific answers in follow-up turns
- Image accessible throughout conversation
- Different prompts produce different responses

**Fail:**
- Image inaccessible in follow-up turns
- Same generic response regardless of follow-up question
- Error related to #6431 image history stripping
