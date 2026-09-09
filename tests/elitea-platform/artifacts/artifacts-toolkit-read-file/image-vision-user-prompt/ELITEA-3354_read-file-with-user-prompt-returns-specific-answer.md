---
id: ELITEA-3354
title: "read_file with user_prompt for PNG Image Returns Specific Answer"
priority: critical
type: functional
module: artifacts-toolkit-read-file
status: draft
execution_type: manual
tags: [feat:artifacts, feat:image-vision, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6530]
---
# ELITEA-3354: read_file with user_prompt for PNG Image Returns Specific Answer

**Module:** Artifacts Toolkit Read File · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that `read_file` with `extra_params={"user_prompt": "..."}` for a PNG image returns an answer to the specific question, not a generic caption.

**Coverage:**
- Custom `user_prompt` is passed to the vision API
- Response directly answers the user's question
- Generic caption behavior replaced when `user_prompt` provided

## Preconditions

- Logged in to dev environment
- Artifact Toolkit with `read_file` enabled
- Multimodal LLM configured (Claude Sonnet 4.5/4.6 or GPT-4 Vision)
- `test_chart.png` uploaded to bucket `test` (image containing a bar chart with values)

## Test Data

| File | Content | user_prompt |
|---|---|---|
| test_chart.png | Bar chart showing Q1=100, Q2=150, Q3=200 | "What is the Q2 value shown in this chart?" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `read_file` on `test_chart.png` with `extra_params={"user_prompt": "What is the Q2 value shown in this chart?"}` | Tool executes successfully. |
| 2 | Examine the response content. | Response directly answers "150" or "The Q2 value is 150" — not a generic description of the chart. |
| 3 | Verify response focuses on the specific question asked. | Response does not include unrelated chart description unless relevant to the question. |

## Expected Final State

The vision model responds with the specific answer to the question ("150" or similar), not a generic image caption.

## Pass/Fail Criteria

**Pass:**
- Response contains the answer to the specific question
- Response is concise and focused on the question asked

**Fail:**
- Response is a generic image description ignoring the question
- Custom `user_prompt` is ignored
- Error returned when `user_prompt` is provided
