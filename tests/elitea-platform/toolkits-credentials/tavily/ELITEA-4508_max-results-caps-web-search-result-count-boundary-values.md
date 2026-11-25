---
id: ELITEA-4508
title: "Verify Max Results caps web_search result count at configured value, including boundary values"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A Tavily toolkit exists with a valid credential, attached to an agent or usable from the toolkit Test page

## Test Data

| Field | Value |
|-------|-------|
| Toolkit setting | Max Results |
| Test values | 1 (min), 5 (default), 10 (max) |
| Query | A broad topic known to return many results (e.g. "technology news") |
| Narrow query | A topic with very few real results (e.g. an obscure niche subject) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Max Results to 1 and run the broad query via `web_search` | Exactly 1 result is returned, never 0 and never more than 1 |
| 2 | Set Max Results to 10 and run the same broad query | Up to 10 results are returned |
| 3 | Set Max Results to 5 (default) and run the same broad query | Result count does not exceed 5 |
| 4 | Lower Max Results on an existing toolkit without changing anything else, then re-run the same query | Result count decreases compared to the prior higher-setting run |
| 5 | Run the narrow query with Max Results set to 10 | Toolkit returns only the real available results (e.g. 2) without erroring or padding the output |

## Expected Final State

The toolkit's Max Results setting is confirmed to be a real functional cap, not a cosmetic field.

## Pass/Fail Criteria

**Pass:**
- Result counts match the configured Max Results value at both bounds and mid-range
- Narrow queries return fewer-than-max results without error

**Fail:**
- Result count ignores the Max Results setting at any tested value
- A narrow query errors or pads results
