---
id: ELITEA-4532
title: "Verify required-field validation and the Search-Depth-vs-toolkit-ceiling interaction on the Test page"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid API key, open on its "Test Toolkit" page

## Test Data

| Field | Value |
|-------|-------|
| Web search Query | Empty |
| Web crawl / Web map Url | Empty |
| Toolkit Max Search Depth | basic, then advanced |
| Per-call Search Depth | advanced |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Leave Query empty on Web search and attempt to run | Run is blocked with a clear required-field message, not a silent no-op |
| 2 | Leave Url empty on Web crawl and Web map and attempt to run | Same required-field validation blocks the run |
| 3 | With the toolkit's Max Search Depth at "basic", set per-call Search Depth to "advanced" and run | Rejected or silently coerced back to basic — the per-call request cannot exceed the toolkit ceiling |
| 4 | Change the toolkit's Max Search Depth to "advanced" and repeat | "Advanced" is now accepted |
| 5 | Populate Instructions on Web crawl/Web map and run with a valid URL | Call succeeds; no UI error suggests disallowed increased cost |

## Expected Final State

Required-field validation and the Search Depth ceiling interaction are both confirmed on the Test page.

## Pass/Fail Criteria

**Pass:**
- Missing required fields block the run
- The Search Depth ceiling is enforced per-call

**Fail:**
- A run proceeds with a missing required field
- A per-call "advanced" request bypasses a "basic" ceiling
