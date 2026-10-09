---
id: ELITEA-3729
title: "Verify banner messages match actual indexing results"
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
- User has indexes with various outcomes

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Scenarios | Successful, partial success, failed |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Complete a successful index | Banner shows success message |
| 2 | Verify message accuracy | Indexed/skipped counts in banner match actual data |
| 3 | Complete a partial success index | Banner reflects partial status |
| 4 | Verify counts are accurate | Numbers shown match actual indexed/skipped/failed |

## Expected Final State

Banner messages accurately reflect the actual indexing results with correct counts.

## Pass/Fail Criteria

**Pass:**
- Banner counts match actual indexed/skipped/failed numbers
- Message accurately describes the outcome

**Fail:**
- Counts in banner don't match reality
- Message is misleading or inaccurate
