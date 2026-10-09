---
id: ELITEA-3723
title: "Verify stale indexing runs are detected and marked as failed"
priority: high
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Backend team can simulate a dead/stuck indexing worker (or wait for natural timeout)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Staleness threshold | System-configured timeout period |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start indexing that will become stuck/dead | Indexing shows "in_progress" |
| 2 | Simulate worker death or disconnect | Worker stops without proper completion |
| 3 | Wait for staleness detection period | System detects stale run |
| 4 | Verify index status | Status changes from "in_progress" to "failed" |
| 5 | Verify user is informed | User can see the run failed (not perpetual spinner) |

## Expected Final State

Stale/dead indexing runs are automatically detected and marked as failed within a reasonable time.

## Pass/Fail Criteria

**Pass:**
- Stale run is detected and status updated to "failed"
- Detection occurs within reasonable timeframe (not 2 hours)

**Fail:**
- Index remains "in_progress" indefinitely
- User sees spinner for hours with no status update
