---
id: ELITEA-2888
title: "Automated: Configuration persistence after page reload"
priority: high
type: automated
module: indexing/save-reindex
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2888: Configuration persistence after page reload

**Module:** indexing/save-reindex · **Priority:** high · **Type:** automated

**Objective:** Verify that saved configuration persists across page reloads.

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
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays with current saved values (Progress Step = 50, Clean Index = unchecked) |
| 2 | Modify Progress Step to 85 and check Clean Index checkbox | "Save" and "Save & Reindex" buttons appear |
| 3 | Click "Save" button | Success notification appears; buttons change to "Reindex" only |
| 4 | Refresh the browser page (F5 or Ctrl+R) | Page reloads |
| 5 | Navigate back to the same index Configuration tab | Configuration loads successfully |
| 6 | Verify saved values are displayed | Progress Step = 85, Clean Index = checked |
| 7 | Verify form is in clean state | Only "Reindex" button displayed |

---

## Expected Final State

Saved configuration persists across page reload. Form loads in clean state with saved values.

---

## Pass/Fail Criteria

**Pass:**
- Saved values persist after page reload
- Form loads in clean state (only "Reindex" button)
- No data loss
- All saved fields display correct values

**Fail:**
- Values revert to original after reload
- Form shows dirty state incorrectly after reload
- Configuration corrupted or lost
