---
id: ELITEA-4104
title: "[EliteaAI/elitea_issues#5889] ADO Toolkit: Image Description Caching (MD5)"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5889, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend]
requirements: [EliteaAI/elitea_issues#5889]
---

# ELITEA-4104: ADO Toolkit — Image Description Caching by MD5

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that extracted image descriptions are cached and reused to avoid redundant LLM calls.

## Preconditions

- ADO toolkit configured with `process_images: true`
- LLM vision model available
- Tool supports MD5-based caching
- Multiple comments with duplicate images available

## Test Data

| Scenario | Image | Cache Key |
|----------|-------|-----------|
| Duplicate URL | Same image URL | MD5 hash of URL |
| Same image, different URL | Identical binary | Dedup on binary? |
| Different images | Different URLs | Different keys |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call get_comments on work item with same image URL appearing twice. | Tool processes first image; calls LLM vision model. |
| 2 | Verify description cached by image URL MD5. | Cache entry created with hash as key. |
| 3 | Process second occurrence of same image URL. | Cache hit; description reused; LLM not called again. |
| 4 | Call get_comments again in new session. | Cache persists; duplicate not re-processed. |
| 5 | Verify cache lookup reduces LLM API calls. | LLM call count matches unique images, not total. |
| 6 | Test with different images: cache miss for new URL. | New image triggers LLM call; cache miss logged. |
| 7 | Test cache expiration (if applicable). | Old cache entries removed after timeout. |
| 8 | Test cache reset: agent restart clears cache. | Cache cleared; next call re-processes images. |

## Expected Final State

- Descriptions cached by image URL MD5
- Duplicate URLs reuse cached descriptions
- Cache persists across multiple get_comments calls
- LLM calls reduced by caching (N unique images = N LLM calls)
- New images trigger LLM call (cache miss)
- Cache cleared on agent restart
- No stale cached data

## Pass/Fail Criteria

**Pass:** Cache working; duplicates reused; LLM calls reduced; cache persists and clears correctly.  
**Fail:** LLM called for duplicates; cache not persisting; stale cache used; cache not clearing.
