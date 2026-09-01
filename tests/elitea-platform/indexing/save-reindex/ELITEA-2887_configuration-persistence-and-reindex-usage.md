---
id: ELITEA-2887
title: "Configuration persistence and reindex usage"
priority: high
type: functional
module: indexing/save-reindex
status: ready
execution_type: manual
tags: [feat:indexer, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2887: Configuration persistence and reindex usage

**Module:** indexing/save-reindex · **Priority:** high · **Type:** functional

**Objective:** Verify that saved configuration persists across page reloads and that manual reindexing operations use the latest saved configuration.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit with at least one indexed index (contains data).
- Index Configuration tab is accessible.

---

## Test Data

| Field | Original Value | New Value |
|-------|----------------|-----------|
| Progress Step | 50 | 85 |
| Clean Index | unchecked | checked |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Save and Persistence** | | |
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays with current saved values (Progress Step = 50, Clean Index = unchecked) |
| 2 | Modify Progress Step to 85 and check Clean Index | "Save" and "Save & Reindex" buttons appear |
| 3 | Click "Save" button | Success notification appears; buttons change to "Reindex" only |
| 4 | Refresh the browser page (F5 or Ctrl+R) | Page reloads |
| 5 | Navigate back to the same index Configuration tab | Configuration loads successfully |
| 6 | Verify saved values are displayed | Progress Step = 85, Clean Index = checked |
| 7 | Verify form is clean (no unsaved changes) | Only "Reindex" button displayed |
| **Manual Reindex Uses Saved Config** | | |
| 8 | Note the current "Files indexed" count in the index header | Count is recorded (e.g., "Files indexed: 10") |
| 9 | Click the "Reindex" button (without making new changes) | Reindexing starts with progress indicator |
| 10 | Wait for reindexing to complete | Reindexing completes successfully; status shows "Index is ready!" |
| 11 | Verify reindexing used the saved configuration | Check logs or behavior consistent with Progress Step = 85 and Clean Index = checked |
| 12 | Verify configuration values remain unchanged | Progress Step still 85, Clean Index still checked |
| **Unsaved Changes NOT Used by Manual Reindex** | | |
| 13 | Modify Progress Step to 100 (do NOT save) | "Save" and "Save & Reindex" buttons appear |
| 14 | Do NOT click Save; instead click browser back/navigate away | Unsaved changes warning may appear; confirm navigation |
| 15 | Return to index Configuration tab | Form resets to last saved state (Progress Step = 85) |
| 16 | Click "Reindex" button | Reindexing uses last saved config (85), not the unsaved 100 |

---

## Expected Final State

- Saved configuration persists across page reloads
- Manual "Reindex" button uses the latest saved configuration
- Unsaved changes are NOT used by reindexing operations

---

## Pass/Fail Criteria

**Pass:**
- Saved values persist after page reload
- Form loads in clean state after reload
- Manual reindex uses last saved configuration
- Unsaved changes do not affect reindexing
- No data loss or corruption

**Fail:**
- Values revert to original after reload
- Form shows dirty state incorrectly after reload
- Reindex uses unsaved/wrong configuration
- Configuration corrupted or lost
