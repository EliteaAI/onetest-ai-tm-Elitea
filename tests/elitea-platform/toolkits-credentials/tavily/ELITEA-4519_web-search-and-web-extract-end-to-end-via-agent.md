---
id: ELITEA-4519
title: "Verify web_search and web_extract work end-to-end when the Tavily toolkit is attached to an agent with a valid key"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit configured with a valid API key, attached to an agent

## Test Data

| Field | Value |
|-------|-------|
| Prompt 1 | A question requiring current information (e.g. "What's today's top tech news?") |
| Prompt 2 | A request to read/extract a specific valid public URL |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Ask the agent Prompt 1 | Agent calls `web_search` and returns an answer referencing search results, with no exception or crash |
| 2 | Ask the agent Prompt 2 | Agent calls `web_extract` and returns content derived from that page |
| 3 | Inspect the visible tool output, trace, and chat transcript for both calls | The configured API key is never exposed anywhere in these surfaces |

## Expected Final State

Both `web_search` and `web_extract` function correctly end-to-end via an agent, with no key leakage.

## Pass/Fail Criteria

**Pass:**
- Both tool calls succeed with usable results
- The key is never exposed

**Fail:**
- Either call fails or crashes
- The key appears anywhere in tool output, trace, or transcript
