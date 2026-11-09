---
id: ELITEA-4525
title: "Verify non-http/https and malformed single-URL input is rejected cleanly for web_crawl and web_map"
priority: critical
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

| Case | Value |
|------|-------|
| Non-http/https | `ftp://example.com` |
| Malformed | `not-a-valid-url` |
| Non-resolving domain | An http/https URL pointing to a random non-existent hostname |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | For Web crawl, enter `ftp://example.com` in Url and run | Clean rejection message naming the offending value, stating only http/https is allowed |
| 2 | For Web crawl, enter `not-a-valid-url` and run | Same clean rejection |
| 3 | Repeat steps 1-2 for Web map's Url field | Identical, consistent error wording and behavior as Web crawl |
| 4 | For both tools, enter an http/https URL with a non-resolving hostname | A clear network/resolution-failure message is returned, not a raw timeout exception or indefinite hang |

## Expected Final State

Both Web crawl and Web map reject invalid URL schemes and malformed/non-resolving URLs consistently and cleanly.

## Pass/Fail Criteria

**Pass:**
- All invalid-URL cases produce clean, consistent messages across both tools

**Fail:**
- Any case produces a raw exception, an indefinite hang, or inconsistent wording between the two tools
