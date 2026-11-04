---
id: ELITEA-4438
title: "Verify no data leakage between different run analytics pages"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, data-isolation, security]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Skill has multiple runs in history
- Each run has different distinguishable token/cost values
- User can access multiple run analytics pages

## Test Data

| Field | Value |
|-------|-------|
| Run A | Tokens: 1000, Cost: $0.05 |
| Run B | Tokens: 500, Cost: $0.02 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Run History | Run History displays |
| 2 | Open Analytics for Run A | Run A analytics opens |
| 3 | Note Run A values: tokens = 1000, cost = $0.05 | Values recorded |
| 4 | Note Run A metadata: date, version, model | Metadata recorded |
| 5 | Close analytics or navigate away | Leave Run A analytics |
| 6 | Open Analytics for Run B | Run B analytics opens |
| 7 | Verify Run B values: tokens = 500, cost = $0.02 | Different values displayed |
| 8 | Verify Run B metadata different from Run A | Different date/time |
| 9 | Switch between tabs on Run B analytics | Tab switching works |
| 10 | Verify all tabs show Run B data only | No Run A data appears |
| 11 | Navigate back to Run A analytics | Return to Run A |
| 12 | Verify Run A displays original values | tokens = 1000, cost = $0.05 |
| 13 | Verify no mixing of Run A and Run B data | Data isolation maintained |
| 14 | Verify backend filters by run_id properly | Correct run scope enforced |

## Expected Final State

Data isolation:
- Each analytics page displays ONLY data for its specific run
- No mixing of data between Run A and Run B
- Run scope strictly enforced by run_id
- Closing and reopening analytics reloads correct data
- Backend filtering works correctly

## Pass/Fail Criteria

**Pass:**
- Each analytics page shows only its run's data
- No data mixing between runs
- Run A and Run B values remain distinct
- Backend run_id filtering works
- Data isolation perfect

**Fail:**
- Data from Run A appears in Run B analytics
- Data mixing detected
- Run A values change unexpectedly
- Backend filtering broken
- Cross-run contamination
