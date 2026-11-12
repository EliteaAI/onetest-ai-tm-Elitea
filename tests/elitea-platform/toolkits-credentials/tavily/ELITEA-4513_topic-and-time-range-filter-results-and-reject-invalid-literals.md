---
id: ELITEA-4513
title: "Verify web_search Topic and Time Range filter results correctly and reject invalid literal values"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit exists with a valid credential, usable from the Test page or an agent

## Test Data

| Field | Value |
|-------|-------|
| Query | A topic with both reference and news coverage (e.g. "electric vehicles") |
| Topic values | general (default), news, finance, invalid value (e.g. "art") |
| Time Range values | day, week, month, year, invalid value (e.g. a literal date "2026-09-22") |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Run the query with Topic at default | Results show a blend of reference and news-style sources |
| 2 | Re-run with Topic="news" | Results shift toward news-style/dated sources |
| 3 | Re-run with Topic="finance" | Results shift toward financial/market sources, distinct from both "general" and "news" |
| 4 | Run a time-sensitive query with no Time Range set | Results span a range of dates |
| 5 | Re-run the same query with Time Range="week" | All results fall within that window; older results from step 4 are excluded |
| 6 | Run a query on a topic with little recent coverage, Time Range="day" | Toolkit returns an honest empty/few-results response, not older results anyway |
| 7 | Combine Topic="news" with a Time Range filter | Both filters apply together, narrowing to recent news specifically |
| 8 | Enter an invalid Topic value (e.g. "art") on the Test page and run | Run is rejected with a clear error naming the valid options, not a silent no-op |
| 9 | Enter an invalid Time Range value (a specific date string) on the Test page and run | Field rejects it with a clear error; confirm the field only accepts the 4 relative windows, not a specific date or custom range |
| 10 | Inspect whether Topic/Time Range are dropdowns or free-text inputs | Document whether input is constrained by a picker or only validated on submission |

## Expected Final State

Topic and Time Range are confirmed as real functional filters restricted to their documented literal value sets.

## Pass/Fail Criteria

**Pass:**
- Topic and Time Range measurably change result content/recency as described
- Invalid values are rejected with a clear message

**Fail:**
- Topic or Time Range has no observable effect
- An invalid value is silently accepted
- The filter silently fails without indication
