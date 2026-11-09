---
id: ELITEA-4516
title: "Verify web_extract correctly attributes each result to its source URL across multiple URLs in one call"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit exists with a valid credential; 3 distinct public URLs with clearly different, identifiable content

## Test Data

| Field | Value |
|-------|-------|
| URLs | 3 distinct URLs (e.g. unrelated Wikipedia articles) |
| Broken URL | A deliberately broken/non-existent URL |
| Duplicate | The same URL submitted twice in one call |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Submit all 3 URLs in one `web_extract` call | Response contains 3 distinct content blocks, each clearly attributable to its correct source URL |
| 2 | Inspect each returned block's content | Each block's content actually matches its own URL's topic, with no cross-contamination |
| 3 | Submit the same 3 URLs in a different order | Results come back correctly re-attributed/re-ordered to match the new input order |
| 4 | Submit the broken URL alongside 2 valid URLs in one call | The 2 valid URLs still return correct content; the broken one is reported with a clear per-URL error, not a total call failure |
| 5 | Submit the duplicate URL twice in one call | Toolkit handles this gracefully (returns content once or twice) without erroring |

## Expected Final State

Multi-URL web_extract calls are confirmed to return correctly attributed, non-mixed results per URL.

## Pass/Fail Criteria

**Pass:**
- Each result block is correctly attributed to its own URL in any submission order
- A broken URL fails only its own entry
- Duplicates do not crash the call

**Fail:**
- Content is mixed, dropped, or misattributed between URLs
- One broken URL fails the entire call
