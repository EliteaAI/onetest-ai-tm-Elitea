---
id: ELITEA-2888
title: "Configuration Persistence and Reuse"
priority: high
type: automated
module: indexing/save-reindex
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2888: Configuration Persistence and Reuse

**Module:** indexing/save-reindex · **Priority:** high · **Type:** automated

**Objective:** Verify that saved configuration persists across page reloads and is correctly used by manual reindex operations.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing index with Configuration tab accessible.

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
| **CONFIGURATION PERSISTENCE** | | |
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays with current saved values (Progress Step = 50, Clean Index = unchecked) |
| 2 | Modify Progress Step to 85 and check Clean Index checkbox | "Save" and "Save & Reindex" buttons appear |
| 3 | Click "Save" button | Success notification appears; buttons change to "Reindex" only |
| 4 | Refresh the browser page (F5 or Ctrl+R) | Page reloads |
| 5 | Navigate back to the same index Configuration tab | Configuration loads successfully |
| 6 | Verify saved values are displayed | Progress Step = 85, Clean Index = checked |
| 7 | Verify form is in clean state | Only "Reindex" button displayed |
| **MANUAL REINDEX USES SAVED CONFIG** | | |
| 8 | Click the "Reindex" button (without modifying any fields) | Reindex operation starts |
| 9 | Verify reindex starts with current config | Index status changes to "Indexing..." |
| 10 | Wait for reindex to complete | Status returns to "Index is ready!" |
| 11 | Navigate to Configuration tab | Configuration tab loads |
| 12 | Verify configuration still shows saved values | Progress Step = 85, Clean Index = checked |
| 13 | Verify last reindex used these settings | Reindex completed with saved configuration (no reset to defaults) |

---

## Expected Final State

Saved configuration persists across page reload and is correctly used by manual reindex operations without modification.

---

## Pass/Fail Criteria

**Pass:**
- Saved values persist after page reload
- Form loads in clean state with saved values
- Manual reindex uses last saved configuration
- Configuration remains unchanged after reindex

**Fail:**
- Configuration lost after page reload
- Reindex uses default or incorrect configuration
- Saved values changed unexpectedly after reindex

---

## Notes

**Source functional tests:** ELITEA-2888 (Configuration persistence after reload), ELITEA-2889 (Manual reindex uses saved config)

**Regression rationale:** Consolidates configuration persistence validation into one flow. Both tests validate configuration durability: persistence across page reload ensures config is saved to backend, and manual reindex using saved config ensures that config is correctly retrieved and applied. Testing together validates the complete config lifecycle: save → persist → reload → reuse.

**Selected checkpoints:** Config saved successfully; page reload; config values persisted; form in clean state; manual reindex starts; reindex uses saved config (not defaults); config unchanged after reindex.
