---
id: ELITEA-3725
title: "Verify indexing handles large datasets without memory issues"
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
- User has access to a large data source (1000+ documents)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Document count | 1000+ documents |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start indexing for large data source | Indexing begins |
| 2 | Monitor progress over time | Progress updates periodically |
| 3 | Wait for completion | Indexing completes without crashing |
| 4 | Verify all documents indexed | Count matches source |

## Expected Final State

Large dataset is indexed successfully without out-of-memory errors or crashes.

## Pass/Fail Criteria

**Pass:**
- Indexing completes successfully for large dataset
- No memory errors or crashes occur

**Fail:**
- Indexing fails with memory-related errors
- System becomes unresponsive during indexing
