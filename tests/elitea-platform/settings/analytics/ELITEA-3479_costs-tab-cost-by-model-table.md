---
id: ELITEA-3479
title: "Costs Tab Cost by Model Table"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3479: Costs Tab Cost by Model Table

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Cost by Model table shows Display Names and proper cost breakdown.

## Preconditions

- Logged into {{base_url}}
- Project has LLM calls with multiple models
- Navigate to Settings → Analytics → Costs

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Cost by Model" section. | Table visible with per-model cost breakdown. |
| 2 | Verify table columns match Cost by User. | Same columns: MODEL, TOTAL COST, INPUT/OUTPUT/CACHE costs, SHARE. |
| 3 | Verify MODEL column shows Display Names. | Friendly model names shown (e.g., "Bedrock-GPT-5.6-Luna"), not raw identifiers. |
| 4 | Verify costs use 6-decimal precision. | All cost values formatted consistently. |
| 5 | Verify SHARE percentages sum to ~100%. | Total model cost shares equal approximately 100%. |
| 6 | Compare total with Cost by User total. | Sum of model costs equals sum of user costs. |

## Pass/Fail Criteria

**Pass:** Display Names shown, consistent formatting, totals match across breakdowns.
**Fail:** Raw model names, formatting inconsistent, or totals don't reconcile.
