---
id: ELITEA-2881
title: "Save & Reindex validates and saves config first then starts reindexing"
priority: critical
type: functional
module: indexing/save-reindex
status: ready
execution_type: manual
tags: [feat:indexer, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2881: Save & Reindex validates and saves config first then starts reindexing

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** functional

**Objective:** 

---


## Preconditions

- User is logged in to `{{base_url}}`
- An existing toolkit with at least one index containing indexed files
- Index Configuration tab is accessible

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/toolkits/all/{toolkit_id}/index/{index_name}` |
| Modified Chunking Config | `{ ".pdf": { "max_tokens": 1024 } }` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays with current settings |
| 2 | Modify the Chunking Config JSON (change max_tokens value) | "Save" and "Save & Reindex" buttons appear |
| 3 | Click "Save & Reindex" button | Button click is registered |
| 4 | Verify configuration is saved first | Success notification for save appears |
| 5 | Verify reindexing starts immediately after save | Index status changes to "Indexing..." with progress indicator |
| 6 | Wait for reindexing to complete | Status returns to "Index is ready!" |
| 7 | Open Configuration tab and verify saved config | Chunking Config shows the modified max_tokens value |

## Expected Final State

Configuration is saved with new Chunking Config, and reindexing completes using the newly saved configuration.

## Pass/Fail Criteria

**Pass:**
- Configuration saves before reindexing starts
- Reindexing uses the newly saved configuration
- Both save and reindex complete successfully

**Fail:**
- Reindexing starts before/without saving
- Configuration is not persisted after reindex
- Either operation fails
