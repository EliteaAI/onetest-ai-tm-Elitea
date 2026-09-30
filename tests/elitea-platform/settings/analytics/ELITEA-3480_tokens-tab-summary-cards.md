---
id: ELITEA-3480
title: "Tokens Tab Summary Cards Display"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3480: Tokens Tab Summary Cards Display

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Tokens tab displays all token metrics including cache tokens (previously missing).

## Preconditions

- Logged into {{base_url}}
- Project has LLM activity with token consumption
- Navigate to Settings → Analytics → Tokens

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click on Tokens tab. | Tokens tab loads with 5 metric cards. |
| 2 | Verify TOTAL TOKENS card. | Shows "input + output tokens" count (e.g., "34.4K"). |
| 3 | Verify INPUT TOKENS card. | Shows prompt tokens count with label "prompt tokens". |
| 4 | Verify OUTPUT TOKENS card. | Shows completion tokens count with label "completion tokens". |
| 5 | Verify CACHE READ card. | Shows cache read tokens count (was previously missing from read-side model). |
| 6 | Verify CACHE WRITE card. | Shows cache write tokens count. |
| 7 | Verify Total = Input + Output. | TOTAL TOKENS approximately equals INPUT + OUTPUT (cache tokens separate). |
| 8 | Verify large numbers use K/M suffix. | Values like "34.4K" for thousands, "1.2M" for millions. |

## Pass/Fail Criteria

**Pass:** All 5 token cards display including cache read/write, formatting uses K/M suffixes.
**Fail:** Cache token cards missing, totals don't add up, or formatting incorrect.
