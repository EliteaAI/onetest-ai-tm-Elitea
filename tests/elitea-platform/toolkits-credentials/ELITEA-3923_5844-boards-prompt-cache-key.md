---
id: ELITEA-3923
title: "[EliteaAI/elitea_issues#5844] ADO Boards: Same Image Different Prompt"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5844, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend, caching]
requirements: [EliteaAI/elitea_issues#5844]
---

# ELITEA-3923: ADO Boards — Same Image with Different Prompts

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that changing prompt triggers new LLM call for same image (prompt in cache key).

## Preconditions

- ADO toolkit configured with `process_images: true`
- Work item with comment containing image
- Same toolkit session
- LLM/tool logs visible

## Test Data

| Call | Prompt | Expected |
|------|--------|----------|
| Call 1 | "short caption" | LLM call 1 |
| Call 2 | "detailed accessibility description" | LLM call 2 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_comments(..., process_images=true, image_description_prompt="short caption")`. | Comments retrieved; image described with short prompt. |
| 2 | Check logs: verify first LLM vision call. | LLM called with short prompt. |
| 3 | In same session, call again with `image_description_prompt="detailed accessibility description"`. | Comments retrieved again. |
| 4 | Verify second call triggers new LLM vision request (not cache hit). | Second LLM call logged. |
| 5 | Compare descriptions: verify prompt influence. | Second description is detailed and includes accessibility info. |
| 6 | Confirm first description is NOT reused. | Descriptions are different; second is more detailed. |
| 7 | Verify LLM calls correspond to prompts. | Logs show 2 LLM requests with different prompts. |

## Expected Final State

- New LLM call on prompt change
- Description reflects new prompt
- Two separate LLM calls logged
- Descriptions differ based on prompt
- Cache key includes both image and prompt

## Pass/Fail Criteria

**Pass:** New LLM call on prompt change; descriptions differ; 2 calls logged.  
**Fail:** Cached description reused; descriptions identical; only 1 call logged.
