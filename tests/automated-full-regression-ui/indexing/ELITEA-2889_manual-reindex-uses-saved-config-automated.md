---
id: ELITEA-2889
title: "Automated: Manual reindex uses last saved configuration"
priority: high
type: automated
module: indexing/save-reindex
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2889: Manual reindex uses last saved configuration

**Module:** indexing/save-reindex · **Priority:** high · **Type:** automated

**Objective:** Verify that manual reindexing operations use the latest saved configuration, not unsaved changes.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit with at least one indexed index (contains data).
- Index Configuration tab is accessible.

---

## Test Data

| Field | Original Value | Saved Value | Unsaved Value |
|-------|----------------|-------------|---------------|
| Progress Step | 50 | 85 | 100 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Save Configuration** | | |
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays (Progress Step = 50) |
| 2 | Modify Progress Step to 85 | "Save" and "Save & Reindex" buttons appear |
| 3 | Click "Save" button | Configuration saved successfully |
| **Reindex Uses Saved Config** | | |
| 4 | Click the "Reindex" button (without making new changes) | Reindexing starts with progress indicator |
| 5 | Wait for reindexing to complete | Reindexing completes successfully; status shows "Index is ready!" |
| 6 | Verify configuration values remain unchanged | Progress Step still 85 |
| **Unsaved Changes NOT Used** | | |
| 7 | Modify Progress Step to 100 (do NOT save) | "Save" and "Save & Reindex" buttons appear |
| 8 | Navigate away without saving (click browser back or another tab) | Navigation occurs (unsaved changes warning may appear; confirm navigation) |
| 9 | Return to index Configuration tab | Form resets to last saved state (Progress Step = 85) |
| 10 | Click "Reindex" button | Reindexing starts |
| 11 | Verify reindexing uses last saved config (85), not the unsaved 100 | Reindex completes successfully using saved configuration |

---

## Expected Final State

Manual "Reindex" button uses the latest saved configuration. Unsaved changes are NOT used by reindexing operations.

---

## Pass/Fail Criteria

**Pass:**
- Manual reindex uses last saved configuration (85)
- Unsaved changes (100) do not affect reindexing
- Configuration values remain unchanged after reindex
- Reindex completes successfully

**Fail:**
- Reindex uses unsaved/wrong configuration
- Unsaved changes affect reindexing operation
- Configuration corrupted during reindex
