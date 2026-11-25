---
id: ELITEA-4531
title: "Verify Max Page Chars truncates extracted content at the configured length with a clear truncation marker"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid credential, a long public page known to exceed a small test value

## Test Data

| Field | Value |
|-------|-------|
| Max Page Chars | 500 (small), 20000 (default), 100000 (large) |
| Long page | A page longer than 500 characters |
| 2 pages of different lengths | Extracted together in one call |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Max Page Chars to 500, extract the long page | Content is cut at approximately that length with a clear truncation marker, not silently cut |
| 2 | Set Max Page Chars to 20000 (default), extract a page shorter than that | Full content returned, no truncation marker |
| 3 | Set Max Page Chars to 100000, extract the same long page | More content returned, proportional to the increase (page permitting) |
| 4 | Extract 2 pages of very different lengths in one call with a moderate Max Page Chars | Each page is truncated independently according to its own length, not one shared/combined truncation |

## Expected Final State

Max Page Chars is confirmed as a real per-page truncation boundary with clear user-facing indication.

## Pass/Fail Criteria

**Pass:**
- Truncation occurs at approximately the configured length with a visible marker
- Truncation applies independently per URL in multi-URL calls

**Fail:**
- Content is silently truncated with no marker
- Truncation is shared/combined across URLs instead of independent
