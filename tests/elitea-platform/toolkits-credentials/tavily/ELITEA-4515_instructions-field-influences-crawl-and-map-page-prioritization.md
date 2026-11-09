---
id: ELITEA-4515
title: "Verify Instructions field influences which pages web_crawl and web_map prioritize"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit exists with a valid credential; a real multi-section public site with clearly distinct topic areas (e.g. separate "Pricing" and "Careers" sections)

## Test Data

| Field | Value |
|-------|-------|
| Instructions (targeted) | "find pages about pricing and costs" |
| Instructions (unrelated) | "find recipes" (on a non-food site) |
| Limit | A moderate value |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run `web_crawl` with Instructions empty, moderate Limit | Pages returned spread generally across the site's sections |
| 2 | Re-run with Instructions targeting one specific section, same Limit | Returned pages are noticeably weighted toward that section vs. the untargeted run |
| 3 | Repeat steps 1-2 for `web_map` | The returned URL list shifts similarly toward the targeted section |
| 4 | Run with Instructions unrelated to the site's actual content | Toolkit does not error or fabricate matches; returns a best-effort normal result or a clear indication nothing matched |

## Expected Final State

Instructions is confirmed to be a real functional influence on crawl/map page prioritization.

## Pass/Fail Criteria

**Pass:**
- Targeted Instructions measurably shift which pages are returned toward the targeted topic for both tools

**Fail:**
- Instructions has no observable effect on either tool's output
- An unrelated instruction causes an error or fabricated result
