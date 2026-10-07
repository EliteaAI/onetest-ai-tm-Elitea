---
id: ELITEA-3728
title: "Verify indexing banner doesn't show spinner forever for dead runs"
priority: medium
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Indexing run has died/become stale

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Max spinner time | Reasonable timeout (not 2 hours) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Observe index with dead/stuck run | Banner shows "indexing in progress" spinner |
| 2 | Wait for staleness detection | System detects dead run |
| 3 | Verify banner updates | Spinner stops, status changes to failed/error |
| 4 | Verify reasonable detection time | Detection occurs within minutes, not hours |

## Expected Final State

Dead indexing runs are detected and banner updates to reflect failure, not infinite spinner.

## Pass/Fail Criteria

**Pass:**
- Spinner stops within reasonable timeframe
- Banner shows appropriate error/failed state

**Fail:**
- Spinner continues for hours
- User cannot distinguish dead run from slow run
