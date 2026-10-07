---
id: ELITEA-3724
title: "Verify re-indexing replaces old data without duplicates"
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
- User has an existing completed index

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Initial documents | 50 documents |
| After source change | 45 documents (5 removed from source) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Note document count of existing index | Count recorded (e.g., 50) |
| 2 | Remove some documents from the source | Source now has fewer documents |
| 3 | Trigger re-indexing | Reindex starts |
| 4 | Wait for reindex to complete | Reindex completes |
| 5 | Verify document count | Count reflects current source (45, not 50 or 95) |
| 6 | Search for removed documents | Removed documents are not found |

## Expected Final State

Re-indexed data reflects current source state without duplicates or orphaned documents.

## Pass/Fail Criteria

**Pass:**
- Document count matches current source count
- Removed documents are no longer searchable
- No duplicate entries exist

**Fail:**
- Old documents persist after reindex
- Document count is doubled (old + new)
- Removed documents still appear in search
