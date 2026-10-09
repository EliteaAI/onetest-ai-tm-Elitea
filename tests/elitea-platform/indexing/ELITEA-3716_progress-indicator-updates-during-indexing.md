---
id: ELITEA-3716
title: "Verify progress indicator updates during indexing"
priority: critical
type: functional
module: indexes
status: ready
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has a toolkit with 200+ documents to index

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Observation window | 5 minutes |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start indexing for a toolkit | Indexing begins |
| 2 | Observe progress indicator for 2 minutes | Progress indicator is visible |
| 3 | Note the indexed count at T=0 | Initial count recorded |
| 4 | Wait 2 minutes and check count again | Count has increased |
| 5 | Continue observing until completion | Progress updates at reasonable intervals |

## Expected Final State

Progress indicator shows increasing document count throughout the indexing process.

## Pass/Fail Criteria

**Pass:**
- Progress indicator updates at least every 2-3 minutes
- Indexed count increases over time
- User can see indexing is actively working

**Fail:**
- Progress stays static for more than 5 minutes while indexing is running
- No visible progress indicator during indexing
- Count jumps from 0 to final number with no intermediate updates
