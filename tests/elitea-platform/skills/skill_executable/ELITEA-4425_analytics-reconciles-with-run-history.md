---
id: ELITEA-4425
title: "Verify analytics data reconciles with Run History row summary"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, integration, s8-dependency]
requirements: [EliteaAI/elitea_issues#6928, EliteaAI/elitea_issues#6927]
---

## Preconditions

- Run History feature (S8) is implemented
- User has skill runs in Run History
- Analytics page is accessible from Run History

## Test Data

| Field | Value |
|-------|-------|
| Dependency | S8 - Skill Run History |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill Run History page | Run History displays with list of runs |
| 2 | Select a specific run row | Run row is identifiable |
| 3 | Note summary data from Run History row | Data noted: duration, status, tokens, cost (if displayed) |
| 4 | Click Analytics for that run | Analytics page opens |
| 5 | Compare Run History duration with Analytics duration | Values consistent |
| 6 | Compare Run History total cost with Analytics TOTAL COST | Values match |
| 7 | Compare Run History tokens with Analytics TOTAL TOKENS | Values match |
| 8 | Compare Run History error status with Analytics Health tab | Error status consistent |
| 9 | Verify if Run History shows error, Health tab shows failed calls | Consistency verified |
| 10 | Verify no data discrepancies between the two views | Perfect reconciliation |

## Expected Final State

Analytics detailed data matches Run History summary:
- Duration consistent between views
- Cost: Run History = Analytics TOTAL COST
- Tokens: Run History = Analytics TOTAL TOKENS
- Error status consistent
- If Run History shows error, Health tab must show failed calls
- No discrepancies

## Pass/Fail Criteria

**Pass:**
- Analytics totals match Run History summary
- Duration consistent
- Cost matches
- Tokens match
- Error status consistent
- If error in Run History, failed calls in Health tab
- Perfect data reconciliation

**Fail:**
- Analytics totals don't match Run History
- Duration mismatch
- Cost mismatch
- Tokens mismatch
- Error status inconsistent
- Error shown in Run History but not in Health tab
- Data discrepancies present
