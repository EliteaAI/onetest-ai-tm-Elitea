---
id: ELITEA-3497
title: "Cross-Page Consistency - Usage vs Analytics"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, issue:6737, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437, EliteaAI/elitea_issues#6737]
---
# ELITEA-3497: Cross-Page Consistency - Usage vs Analytics

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify data consistency between Usage page and Analytics page for same period.

**Coverage:** Bug #6737 - Model call totals mismatch caused by embedding treatment.

## Preconditions

- Logged into {{base_url}}
- Project has varied activity including embedding model calls
- Record the billing period dates from Usage page

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Settings → Usage. | Usage page loads with billing summary. |
| 2 | Note total CALLS value. | Record the number (e.g., 50). |
| 3 | Note "Usage by Model" table entries. | Record all models including embedding models. |
| 4 | Record embedding model call count. | Note text-embedding-3-small or similar count. |
| 5 | Navigate to Settings → Analytics → Overview. | Analytics Overview loads. |
| 6 | Set same date range as Usage billing period. | Custom dates match Usage period. |
| 7 | Note LLM CALLS card value. | Record the number. |
| 8 | Compare Usage CALLS with Analytics LLM CALLS. | Document any difference. |
| 9 | Check Model Usage Breakdown for embeddings. | Note if embedding models are listed. |
| 10 | Calculate expected difference. | Difference should equal embedding model calls if excluded from Analytics. |

## Expected Behavior

Either:
- Both pages include embedding calls (totals match exactly)
- Both pages exclude embedding calls (totals match exactly)
- Clear documentation exists explaining intentional difference

## Pass/Fail Criteria

**Pass:** Totals are consistent OR difference is exactly explained by documented embedding treatment.
**Fail:** Unexplained discrepancy between Usage and Analytics totals.
