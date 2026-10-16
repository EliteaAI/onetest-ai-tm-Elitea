---
id: ELITEA-3921
title: "[EliteaAI/elitea_issues#5844] ADO Boards: Repeated Same Image in Comments"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5844, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend, caching]
requirements: [EliteaAI/elitea_issues#5844]
---

# ELITEA-3921: ADO Boards — Repeated Same Image in Comments

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that identical image repeated in multiple comments is described once and reused from cache in same runtime instance.

## Preconditions

- ADO toolkit configured with `process_images: true`
- `image_description_prompt` is set
- One work item has comments containing the same attachment image more than once, OR multiple comments reference the same image URL
- LLM/tool logs visible
- Same toolkit session

## Test Data

| Location | Image | URL |
|----------|-------|-----|
| Comment 1 | Image.jpg | /attachments/image.jpg |
| Comment 3 | Image.jpg | /attachments/image.jpg |
| Comment 5 | Image.jpg | /attachments/image.jpg |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `get_comments(..., process_images=true)` on work item. | All comments with images retrieved. |
| 2 | Verify returned HTML includes descriptions for all image occurrences. | All three image references have descriptions. |
| 3 | Check logs: count LLM vision API calls. | **Only ONE LLM call** for identical image bytes. |
| 4 | Repeat call in same session on same work item. | Second call completes. |
| 5 | Verify cache reused: no new LLM calls on second invocation. | No additional LLM calls logged. |
| 6 | Confirm all image references still have descriptions. | Descriptions present in both calls. |
| 7 | Verify descriptions are consistent across occurrences. | Same description for all image instances. |

## Expected Final State

- First encounter triggers one description generation
- Repeated occurrences reuse cache
- Returned HTML includes image descriptions as before
- Consistent descriptions across occurrences
- Only one LLM call per unique image-prompt pair

## Pass/Fail Criteria

**Pass:** 1 LLM call; cache reused; descriptions consistent; all occurrences described.  
**Fail:** Multiple LLM calls; cache not used; descriptions inconsistent; missing descriptions.
