---
id: ELITEA-2882
title: "Save & Reindex does not start reindex when validation fails"
priority: critical
type: functional
module: indexing/save-reindex
status: ready
execution_type: manual
tags: [feat:indexer, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2882: Save & Reindex does not start reindex when validation fails

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** functional

**Objective:** 

---


## Preconditions

- User is logged in to `{{base_url}}`
- An existing index with Configuration tab accessible

## Test Data

| Field | Value |
|-------|-------|
| Invalid Chunking Config | `{ ".pdf": { "max_tokens": }` (malformed JSON) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays |
| 2 | Enter invalid JSON in the Chunking Config editor | JSON syntax error is shown (red highlight or inline error) |
| 3 | Click "Save & Reindex" button | JSON disappeared |
| 4 | Verify reindexing does NOT start | Index status remains "Index is ready!" — no progress indicator appears |
| 5 | Verify error message is clear | Error indicates JSON validation failure |

## Expected Final State

Validation error prevents both save and reindex. Index remains unchanged.

## Pass/Fail Criteria

**Pass:**
- Validation error displayed for invalid JSON
- Reindexing does NOT start
- Index data unchanged

**Fail:**
- Reindexing starts despite validation error
- No error message shown
- System crashes or hangs
