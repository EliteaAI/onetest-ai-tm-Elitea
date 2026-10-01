---
id: ELITEA-3614
title: "Tokens Tab Content - Cards and Tables"
priority: critical
type: functional
module: per-run-analytics
status: ready
execution_type: manual
tags: [feat:analytics, eng:frontend, issue:6816, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6816]
---
# ELITEA-3614: Tokens Tab Content - Cards and Tables

**Module:** Per-Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Tokens tab displays all 5 token cards and Usage by User/Model tables.

## Preconditions

- Logged into {{base_url}}
- Per-Run Analytics page open on Tokens tab
- Run had LLM activity

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Per-Run Analytics and click Tokens tab. | Tokens tab content displayed. |
| 2 | Verify TOTAL TOKENS card is present. | Card shows input + output tokens (e.g., "34.4K"). |
| 3 | Verify INPUT TOKENS card is present. | Card shows prompt tokens count. |
| 4 | Verify OUTPUT TOKENS card is present. | Card shows completion tokens count. |
| 5 | Verify CACHE READ TOKENS card is present. | Card shows cache read tokens (may be 0). |
| 6 | Verify CACHE WRITE TOKENS card is present. | Card shows cache write tokens. |
| 7 | Verify large numbers use K/M suffix. | E.g., "34.4K", "1.2M". |
| 8 | Scroll to Usage by User table. | Table displays user(s) with token breakdown. |
| 9 | Scroll to Usage by Model table. | Table displays model(s) with token breakdown. |

## Pass/Fail Criteria

**Pass:** 5 token cards with proper formatting and both tables present.
**Fail:** Any card/table missing or incorrect data.
