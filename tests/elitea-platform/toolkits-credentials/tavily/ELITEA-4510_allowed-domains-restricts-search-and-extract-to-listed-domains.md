---
id: ELITEA-4510
title: "Verify Allowed Domains restricts web_search results and web_extract to only the listed domains"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit exists with a valid credential, attached to an agent or usable from the toolkit Test page

## Test Data

| Field | Value |
|-------|-------|
| Allowed Domains | `wikipedia.org` |
| Second Allowed Domain | A different well-known domain |
| Query | A broad query where other domains would normally outrank the allowed one |
| Unrelated query | A query unrelated to the allowed domain's content |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Allowed Domains to the single domain and run the broad query | Every returned result is from that domain; no other domain appears |
| 2 | Attempt `web_extract` on a URL NOT in Allowed Domains | Extraction is refused with a clear message |
| 3 | Attempt `web_extract` on a URL from the allowed domain | Extraction succeeds normally |
| 4 | Add a second domain to Allowed Domains and re-run | Results/extraction now include both domains, not just the first |
| 5 | Run the unrelated query with Allowed Domains restricted to an unrelated domain | Toolkit returns an empty/no-results response rather than silently ignoring the restriction |
| 6 | Add the same domain to both Allowed Domains and Blocked Domains and run a query | Toolkit does not crash; documented behavior shows which list takes precedence |

## Expected Final State

Allowed Domains is confirmed to be an enforced allow-list excluding every non-listed domain.

## Pass/Fail Criteria

**Pass:**
- Only allowed domain(s) appear in results
- Non-allowed URLs are refused for extraction
- Contradictory allow/block config does not crash the toolkit

**Fail:**
- A non-allowed domain appears in results
- Extraction succeeds on a non-allowed URL
- Contradictory config crashes the toolkit
