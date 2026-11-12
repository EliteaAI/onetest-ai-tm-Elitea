---
id: ELITEA-4514
title: "Verify Max Depth and Limit control the scope of web_crawl and web_map results"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit exists with a valid credential; a real multi-page public site suitable for crawling/mapping

## Test Data

| Field | Value |
|-------|-------|
| Max Depth | 1, 2 |
| Limit | 5, 20 (web_crawl); 20, 50 (web_map) |
| Target site | A documentation site with many linked pages |
| Small site | A site with only ~3 total linked pages |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run `web_crawl` with Max Depth=1, Limit=20 | Returned pages are all one hop from the starting URL |
| 2 | Re-run with Max Depth=2, same Limit | Crawl reaches two-hop pages, returning a broader/different page set than depth=1 |
| 3 | With Max Depth=2, run once with Limit=5 and once with Limit=20 | Limit=5 returns at most 5 pages; Limit=20 returns more (site permitting) |
| 4 | Run the exact same call twice (same URL/depth/limit) | Establish baseline variation between repeated same-parameter runs |
| 5 | Compare depth=1 vs depth=2 result sets against the step-4 baseline | Document whether depth=2 reasonably contains depth=1's pages, consistent with a cumulative link-hop depth |
| 6 | Repeat steps 1-5 for `web_map` | Same proportional Limit effect and depth-containment expectation holds for the returned URL list |
| 7 | Run both tools against the small 3-page site with Max Depth=1, Limit=20 | Only the 3 real pages are returned; no error, no fabricated entries |

## Expected Final State

Max Depth and Limit are confirmed as real, proportional controls over crawl/map scope for both tools.

## Pass/Fail Criteria

**Pass:**
- Limit caps page count proportionally
- Depth increases reach more pages consistent with link-hop traversal
- Small sites return only real pages

**Fail:**
- Limit or Max Depth has no observable effect
- The toolkit errors or fabricates pages on a small site
