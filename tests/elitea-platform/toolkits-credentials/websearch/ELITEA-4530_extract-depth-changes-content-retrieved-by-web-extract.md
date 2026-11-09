---
id: ELITEA-4530
title: "Verify Extract Depth setting changes the content retrieved by web_extract"
priority: high
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit with a valid credential, usable from an agent or the Test page; a real public URL with substantial page content

## Test Data

| Field | Value |
|-------|-------|
| Extract Depth | basic, advanced |
| Target URL | A long, content-rich article |
| Thin page | A near-blank landing page |
| Multi-URL call | 3 URLs extracted together |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | With Extract Depth="basic", extract the content-rich page and note the result | Content returned successfully |
| 2 | Change Extract Depth to "advanced", re-run on the same URL | A measurable difference is observed (e.g. more complete content) compared to basic |
| 3 | Extract the thin page at both depth settings | Neither setting errors or returns misleading content — whatever genuinely exists is returned |
| 4 | Extract 3 URLs together in one call with Extract Depth set | The setting applies consistently across all 3 URLs, not just the first |

## Expected Final State

Extract Depth is confirmed to have a real, observable effect on extracted content across single and multi-URL calls.

## Pass/Fail Criteria

**Pass:**
- "Advanced" produces a measurable content difference from "basic", applied consistently across all URLs in a multi-URL call

**Fail:**
- No observable difference between settings
- The setting only applies to the first URL in a multi-URL call
