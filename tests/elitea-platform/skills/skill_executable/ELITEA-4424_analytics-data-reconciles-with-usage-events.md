---
id: ELITEA-4424
title: "Verify analytics totals match sum of usage_event rows for run"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, data-accuracy, backend-validation]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- Access to usage database
- Skill run has completed and generated usage_event rows
- User is on analytics page for the run

## Test Data

| Field | Value |
|-------|-------|
| Database Table | usage_event |
| Run Identifier | run_id / conversation UUID |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Identify the run_id / UUID for the skill run | Unique identifier obtained |
| 2 | Query usage_event table: `SELECT * FROM usage_event WHERE run_id = '<uuid>'` | All rows for this run retrieved |
| 3 | Calculate aggregate values from query results | Aggregates calculated |
| 4 | Calculate: SUM(input_tokens), SUM(output_tokens), SUM(cache_read_tokens), SUM(cache_write_tokens) | Token sums calculated |
| 5 | Calculate: SUM(input_cost), SUM(output_cost), SUM(cache_read_cost), SUM(cache_write_cost) | Cost sums calculated |
| 6 | Calculate: COUNT(errors), AVG(latency) | Error count and avg latency calculated |
| 7 | Open analytics page for the same run | Analytics page displays |
| 8 | Compare DB token sums with UI TOTAL TOKENS and breakdown | Values match |
| 9 | Compare DB cost sums with UI TOTAL COST and breakdown | Values match |
| 10 | Compare DB error count with UI Health tab ERRORS | Values match |
| 11 | Compare DB avg latency with UI AVG LATENCY | Values match |
| 12 | Verify no double-counting of nested tool/LLM calls | Each call counted once only |

## Expected Final State

Analytics UI data matches DB aggregates:
- UI TOTAL TOKENS = SUM of all usage_event token fields
- UI TOTAL COST = SUM of all usage_event cost fields
- UI error counts = COUNT of usage_event rows with errors
- UI latencies = AVG/SUM of usage_event latency values
- No double-counting
- Perfect data consistency

## Pass/Fail Criteria

**Pass:**
- All UI totals match DB aggregates
- Token sums match: INPUT, OUTPUT, CACHE READ, CACHE WRITE
- Cost sums match: all cost components
- Error counts match
- Latencies match
- No double-counting detected
- Perfect DB-to-UI consistency

**Fail:**
- UI totals don't match DB aggregates
- Token sums mismatch
- Cost sums mismatch
- Error counts mismatch
- Latency calculations wrong
- Double-counting detected
- Data inconsistencies
