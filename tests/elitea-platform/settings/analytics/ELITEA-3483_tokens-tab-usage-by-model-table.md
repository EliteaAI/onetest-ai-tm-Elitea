---
id: ELITEA-3483
title: "Tokens Tab Token Usage by Model Table"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3483: Tokens Tab Token Usage by Model Table

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Token Usage by Model table shows Display Names and complete breakdown.

## Preconditions

- Logged into {{base_url}}
- Project has LLM calls with multiple models
- Navigate to Settings → Analytics → Tokens

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Token Usage by Model" section. | Table visible with per-model token breakdown. |
| 2 | Verify MODEL column shows Display Names. | Friendly names (e.g., "Bedrock-GPT-5.6-Luna"), not raw identifiers. |
| 3 | Verify all token columns present. | TOTAL, INPUT, OUTPUT, CACHE READ, CACHE WRITE, SHARE columns. |
| 4 | Verify token formatting is consistent. | Same K/M format as other tables. |
| 5 | Verify SHARE percentages sum to ~100%. | Total equals approximately 100%. |

## Pass/Fail Criteria

**Pass:** Display Names shown, complete breakdown, consistent formatting.
**Fail:** Raw model names, missing columns, or inconsistent data.
