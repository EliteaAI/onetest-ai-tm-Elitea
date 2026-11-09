---
id: ELITEA-4509
title: "Verify Blocked Domains excludes configured domains from web_search results and web_extract"
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
| Blocked Domains | `wikipedia.org` |
| Second Blocked Domain | A different well-known domain |
| Misspelled domain | `wikipedai.org` (does not exist) |
| Query | A general-knowledge topic likely to surface the blocked domain |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the query with Blocked Domains empty | The target domain appears in the baseline results |
| 2 | Add the target domain to Blocked Domains, save, re-run the identical query | The domain no longer appears anywhere in results |
| 3 | Attempt `web_extract` on a URL from the blocked domain | Extraction is refused with a clear message, not a silent success or silent failure |
| 4 | Add a second domain to Blocked Domains (comma-separated) and re-test | Both domains are excluded simultaneously |
| 5 | Set Blocked Domains to the misspelled domain only, re-run the original query | No error occurs; the real domain is not blocked; nothing unintended is blocked |

## Expected Final State

Blocked Domains is confirmed to be an enforced exclusion list across both `web_search` and `web_extract`.

## Pass/Fail Criteria

**Pass:**
- Blocked domain(s) never appear in search results
- `web_extract` refuses blocked URLs with a clear message
- Multiple blocked domains work together
- A misspelled entry has no unintended effect

**Fail:**
- A blocked domain still appears in results
- `web_extract` silently succeeds/fails on a blocked URL
- A misspelled entry blocks something unintended
