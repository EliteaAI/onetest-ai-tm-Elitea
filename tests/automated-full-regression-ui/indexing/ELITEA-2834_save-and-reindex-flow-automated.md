---
id: ELITEA-2834
title: "Automated: Save & Reindex flow"
priority: critical
type: automated
module: indexing/save-reindex
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2834: Save & Reindex flow

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** automated

**Objective:** Verify that Save & Reindex validates and saves configuration first, then starts reindexing, with success notification.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit with at least one indexed index.
- Index Configuration tab is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Modified Chunking Config | `{ ".pdf": { "max_tokens": 1024 } }` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays with current settings |
| 2 | Modify the Chunking Config JSON (change max_tokens value) | "Save" and "Save & Reindex" buttons appear |
| 3 | Click "Save & Reindex" button | Button click is registered |
| 4 | Verify success notification appears | Toast shows "Configuration saved, reindexing started" or similar |
| 5 | Verify notification auto-dismisses | Notification disappears after timeout |
| 6 | Verify reindexing starts immediately after save | Index status changes to "Indexing..." with progress indicator |
| 7 | Wait for reindexing to complete | Status returns to "Index is ready!" |
| 8 | Navigate to Configuration tab and verify saved config | Chunking Config shows the modified max_tokens value (1024) |

---

## Expected Final State

Configuration saved with new Chunking Config. Reindexing completed using the newly saved configuration. Success notification displayed.

---

## Pass/Fail Criteria

**Pass:**
- Configuration saves before reindexing starts
- Success notification displayed and auto-dismisses
- Reindexing uses the newly saved configuration
- Both save and reindex complete successfully

**Fail:**
- Reindexing starts before/without saving
- No success notification or wrong notification
- Configuration not saved correctly
- Reindexing fails or uses old config
