---
id: ELITEA-4420
title: "Verify Health tab displays Health by Event Type table correctly"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, analytics, health]
requirements: [EliteaAI/elitea_issues#6928]
---

## Preconditions

- User is on skill run analytics page
- Run has completed with health event data
- Run may have succeeded or failed with errors

## Test Data

| Field | Value |
|-------|-------|
| Table Columns | EVENT TYPE, TOTAL ↓, ERRORS, ERROR RATE, AVG LATENCY |
| Event Types | llm, tool, skill |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click "Health" tab | Health tab opens and becomes active |
| 2 | Observe "Health by Event Type" table | Table is visible |
| 3 | Check table headers | Headers: EVENT TYPE, TOTAL ↓, ERRORS, ERROR RATE, AVG LATENCY |
| 4 | Verify event types listed | Common types: "llm", "tool", "skill" (depending on run) |
| 5 | Verify TOTAL column | Count of events per event type |
| 6 | Verify ERRORS column | Count of failed events per type |
| 7 | Verify ERROR RATE column | Percentage: (errors / total) * 100 |
| 8 | Verify ERROR RATE color | Red text if error rate > 0%, normal if 0% |
| 9 | Verify AVG LATENCY column | Average duration in milliseconds (e.g., "406ms") |
| 10 | Cross-reference with usage_event table | Counts and calculations match DB data |

## Expected Final State

Health by Event Type table displays:
- All event types from the run (llm, tool, skill)
- TOTAL: count of events per type
- ERRORS: count of failed events
- ERROR RATE: (errors / total) * 100, shown as percentage
- AVG LATENCY: average duration in ms
- Error rates > 0% shown in red color

## Pass/Fail Criteria

**Pass:**
- Health tab loads successfully
- Table displays all event types from run
- TOTAL counts accurate
- ERRORS count accurate
- ERROR RATE calculated correctly: (errors / total) * 100
- ERROR RATE > 0% shown in red
- AVG LATENCY accurate in milliseconds
- Data matches usage_event table

**Fail:**
- Health tab fails to load
- Missing event types
- Incorrect counts
- ERROR RATE calculation wrong
- Error rates not highlighted in red
- AVG LATENCY incorrect or wrong format
- Data doesn't match usage_event table
