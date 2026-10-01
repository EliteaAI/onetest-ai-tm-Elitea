---
id: ELITEA-3649
title: "Evaluation Analytics Tokens Tab Content"
priority: critical
type: functional
module: evaluation-run-analytics
status: ready
execution_type: manual
tags: [feat:agent_eval, feat:analytics, eng:frontend, issue:6817, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6817]
---
# ELITEA-3649: Evaluation Analytics Tokens Tab Content

**Module:** Evaluation Run Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Tokens tab displays token cards and tables with evaluation-specific data.

## Preconditions

- Logged into {{base_url}}
- Evaluation Analytics page open on Tokens tab

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Evaluation Analytics and click Tokens tab. | Tokens tab content displayed. |
| 2 | Verify TOTAL TOKENS card is present. | Shows input + output tokens. |
| 3 | Verify INPUT TOKENS card is present. | Shows prompt tokens count. |
| 4 | Verify OUTPUT TOKENS card is present. | Shows completion tokens count. |
| 5 | Verify CACHE READ TOKENS card is present. | Shows cache read tokens. |
| 6 | Verify CACHE WRITE TOKENS card is present. | Shows cache write tokens. |
| 7 | Verify large numbers use K/M suffix. | E.g., "34.4K", "1.2M". |
| 8 | Scroll to Usage by User table. | Table displays user(s). |
| 9 | Scroll to Usage by Model table. | Table displays model(s). |

## Pass/Fail Criteria

**Pass:** All token cards and tables present with proper formatting.
**Fail:** Cards/tables missing or incorrect data.
