---
id: ELITEA-3726
title: "Verify index history shows limited runs (not unlimited)"
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
- Index has been run multiple times (10+ runs)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an index with many historical runs | Index detail page loads |
| 2 | Open History view | History displays |
| 3 | Count number of runs shown | Limited number displayed (e.g., last N runs) |
| 4 | Verify oldest runs are not shown if limit exceeded | History is capped |

## Expected Final State

Index history displays a reasonable limited number of runs, not unbounded history.

## Pass/Fail Criteria

**Pass:**
- History shows last N runs (defined limit)
- Page loads quickly without performance issues

**Fail:**
- All historical runs displayed (unbounded)
- Page performance degrades with many runs
