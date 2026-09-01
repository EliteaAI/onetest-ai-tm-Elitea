---
id: ELITEA-2833
title: "Automated: Save without reindex"
priority: critical
type: automated
module: indexing/save-reindex
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.6, automated, regression]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2833: Save without reindex

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** automated

**Objective:** Verify that Save button persists configuration changes without triggering reindexing, and displays success notification.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit with at least one indexed index (contains data).
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
| 2 | Click on an existing index to open its Configuration tab | Configuration tab displays with current saved values |
| 3 | Note the current "Files indexed" count in the index header | Count is recorded (e.g., "Files indexed: 10") |
| 4 | Modify the Progress Step slider from 50 to 75 | "Save" and "Save & Reindex" buttons appear |
| 5 | Click the "Save" button | Save operation completes successfully |
| 6 | Verify success notification appears | Toast notification shows "Configuration saved successfully" or similar |
| 7 | Verify notification auto-dismisses | Notification disappears after timeout (3-5s) |
| 8 | Verify no indexing operation starts | Index status remains "Index is ready!" — no progress indicator |
| 9 | Verify "Files indexed" count remains unchanged | Count is identical to Step 3 |
| 10 | Navigate away and return to the Configuration tab | Progress Step shows 75 (saved value persisted) |
| 11 | Verify form is in clean state | Only "Reindex" button is displayed |

---

## Expected Final State

Configuration saved with new Progress Step value (75). Index data unchanged. Success notification displayed. Form returns to clean state.

---

## Pass/Fail Criteria

**Pass:**
- Save button persists configuration changes
- No indexing operation triggered
- Index data (file count) unchanged
- Success notification displayed and auto-dismisses
- Saved values persist across navigation
- Form returns to clean state after save

**Fail:**
- Indexing starts after clicking Save
- Configuration not persisted
- File count changes
- No success notification or wrong notification
- Form remains dirty after save
