---
id: ELITEA-2833
title: "Save/Reindex Configuration UX"
priority: critical
type: automated
module: indexing/save-reindex
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2833: Save/Reindex Configuration UX

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** automated

**Objective:** Verify the complete Save/Reindex configuration UX flow including button states, Save without reindex, Save & Reindex flow, and validation blocking invalid configurations.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit with at least one indexed index (contains data).
- Index Configuration tab is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Progress Step Original | 50 |
| Progress Step Modified | 75 |
| Valid Chunking Config | `{ ".pdf": { "max_tokens": 1024 } }` |
| Invalid Chunking Config | `{ ".pdf": { "max_tokens": }` (malformed JSON) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **CLEAN STATE & BUTTON VISIBILITY** | | |
| 1 | Navigate to Toolkits & Indexes and select an existing toolkit with indexed data | Toolkit details page opens |
| 2 | Click on an existing index to open its Configuration tab | Configuration tab displays with current saved values |
| 3 | Verify button state when no changes made | Only "Reindex" button is displayed |
| **SAVE WITHOUT REINDEX** | | |
| 4 | Note the current "Files indexed" count in the index header | Count is recorded (e.g., "Files indexed: 10") |
| 5 | Modify the Progress Step slider from 50 to 75 | "Save" and "Save & Reindex" buttons appear (dirty state) |
| 6 | Click the "Save" button | Save operation completes successfully |
| 7 | Verify success notification appears | Toast notification shows "Configuration saved successfully" or similar |
| 8 | Verify notification auto-dismisses | Notification disappears after timeout (3-5s) |
| 9 | Verify no indexing operation starts | Index status remains "Index is ready!" — no progress indicator |
| 10 | Verify "Files indexed" count remains unchanged | Count is identical to Step 4 |
| 11 | Verify form returns to clean state | Only "Reindex" button is displayed |
| **SAVE & REINDEX FLOW** | | |
| 12 | Modify the Chunking Config JSON (change max_tokens to 1024) | "Save" and "Save & Reindex" buttons appear |
| 13 | Click "Save & Reindex" button | Button click is registered |
| 14 | Verify success notification appears | Toast shows "Configuration saved, reindexing started" or similar |
| 15 | Verify notification auto-dismisses | Notification disappears after timeout |
| 16 | Verify reindexing starts immediately after save | Index status changes to "Indexing..." with progress indicator |
| 17 | Wait for reindexing to complete | Status returns to "Index is ready!" |
| 18 | Navigate to Configuration tab and verify saved config | Chunking Config shows the modified max_tokens value (1024) |
| **VALIDATION BLOCKS SAVE & REINDEX** | | |
| 19 | Modify Chunking Config to invalid JSON: `{ ".pdf": { "max_tokens": }` | JSON syntax error is shown (red highlight or inline error) |
| 20 | Click "Save & Reindex" button | Validation attempt occurs |
| 21 | Verify error notification appears | Toast shows validation error message (e.g., "Invalid JSON in Chunking Config") |
| 22 | Verify error message is clear and actionable | Message indicates JSON validation failure |
| 23 | Verify reindexing does NOT start | Index status remains "Index is ready!" — no progress indicator |
| 24 | Verify form state is preserved | Invalid JSON remains in editor; user can correct and retry |
| 25 | Fix the JSON error (add closing brace) | JSON becomes valid |
| 26 | Click "Save & Reindex" again | Operation succeeds this time |
| 27 | Verify success notification appears | Toast shows "Configuration saved, reindexing started" |

---

## Expected Final State

Complete Save/Reindex UX validated: clean state shows only Reindex button; dirty state shows Save + Save&Reindex; Save persists without reindexing; Save&Reindex saves then reindexes; validation blocks invalid configs with clear error messages.

---

## Pass/Fail Criteria

**Pass:**
- Button states correctly reflect form dirty/clean state
- Save button persists configuration without triggering reindexing
- Save & Reindex validates, saves, then starts reindexing
- Validation errors prevent save/reindex operations with clear error messages
- Success notifications displayed and auto-dismiss
- Form state transitions work correctly

**Fail:**
- Incorrect button states displayed
- Save triggers reindexing or Save & Reindex doesn't start reindexing
- Validation allows invalid configuration to be saved
- Error messages unclear or operations fail silently

---

## Notes

**Source functional tests:** ELITEA-2833 (Save without reindex), ELITEA-2834 (Save & Reindex flow), ELITEA-2835 (Validation blocks), ELITEA-2836 (Button states)

**Regression rationale:** Consolidates the complete Save/Reindex configuration UX into one coherent journey. All four aspects are tightly coupled in the UI state machine: button visibility depends on form state, Save vs Save&Reindex have different behaviors, and validation guards both. Testing these together ensures the entire configuration management flow works cohesively from clean state through modifications, saves, and validation.

**Selected checkpoints:** Clean state (Reindex only); Dirty state (Save + Save&Reindex appear); Save without reindex (config persisted, no indexing); Save & Reindex (saves then starts reindex); Validation (invalid JSON blocked with error); Button state transitions; Success notifications.
