---
id: ELITEA-4520
title: "Verify web_crawl and web_map work via the toolkit directly and are not exposed via the chat Web Search toggle"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with all four tools selected, attached to an agent; a chat with the "Web Search" module toggle available

## Test Data

| Field | Value |
|-------|-------|
| Crawl target | A small public site, shallow depth |
| Map target | A small public site |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ask the agent (toolkit attached) to crawl the small site at shallow depth | `web_crawl` executes and returns results without error |
| 2 | Ask the agent to map the small site | `web_map` executes and returns results without error |
| 3 | In a plain chat (not the agent), enable the "Web Search" module toggle and attempt to trigger crawl/map-like behavior purely via chat | Only `web_search`/`web_extract`-style behavior is accessible; no way to trigger a crawl or site-map action through the chat toggle alone |

## Expected Final State

`web_crawl`/`web_map` are confirmed functional only through a directly-attached toolkit, never via the chat-level Web Search toggle.

## Pass/Fail Criteria

**Pass:**
- Crawl/map work when the toolkit is attached to an agent
- The chat Web Search toggle never exposes crawl/map capability

**Fail:**
- Crawl or map fails via the toolkit
- Either is reachable purely through the chat toggle
