---
id: ELITEA-2880
title: "Save button persists configuration without triggering reindex"
priority: critical
type: functional
module: indexing/save-reindex
status: ready
execution_type: manual
tags: [feat:indexer, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2880: Save button persists configuration without triggering reindex

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** functional

**Objective:** Verify that the "Save" button persists configuration changes without triggering reindexing, ensuring the existing index data remains unchanged.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit with at least one index that has been previously indexed (contains data).
- Index Configuration tab is accessible.

---

## Test Data

| Field | Original Value | Modified Value |
|-------|----------------|----------------|
| Progress Step | 50 | 75 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes and select an existing toolkit with indexed data | Toolkit details page opens |
| 2 | Click on an existing index to open its Configuration tab | Configuration tab displays: Clean Index checkbox, Progress Step slider, Chunking Config editor |
| 3 | Note the current "Files indexed" count in the index header | Count is recorded (e.g., "Files indexed: 10") |
| 4 | Modify the Progress Step slider from 50 to 75 | "Save" and "Save & Reindex" buttons appear |
| 5 | Click the "Save" button | Save operation completes successfully |
| 6 | Verify success notification appears | Toast notification shows "Configuration saved successfully" or similar |
| 7 | Verify no indexing operation starts | Index status remains "Index is ready! No documents to index. The index is ready to search." — no progress indicator, no "Indexing..." status |
| 8 | Verify "Files indexed" count remains unchanged | Count is identical to Step 3 (e.g., still "Files indexed: 10") |
| 9 | Navigate away and return to the same index Configuration tab | Progress Step shows 75 (saved value persisted) |
| 10 | Verify form is in clean state | Only "Reindex" button is displayed |

---

## Expected Final State

Configuration is saved with new Progress Step value (75). Index data remains unchanged — no reindexing occurred. Saved configuration persists across navigation.

---

## Pass/Fail Criteria

**Pass:**
- Save button persists configuration changes
- No indexing operation is triggered after clicking "Save"
- Index data (file count) remains unchanged
- Success notification displayed
- Saved values persist across navigation
- Form returns to clean state after save

**Fail:**
- Indexing starts after clicking "Save"
- Configuration changes are not persisted
- File count changes (indicating reindexing occurred)
- No success notification or error shown
- Saved values not preserved after navigation
