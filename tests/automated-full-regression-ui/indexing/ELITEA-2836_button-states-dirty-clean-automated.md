---
id: ELITEA-2836
title: "Automated: Button states - dirty and clean transitions"
priority: critical
type: automated
module: indexing/save-reindex
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.6, regression]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2836: Button states - dirty and clean transitions

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** automated

**Objective:** Verify that UI button states correctly reflect form dirty/clean state transitions.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit with at least one index exists.
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
| **Clean State** | | |
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays with current saved values |
| 2 | Verify button state when no changes made | Only "Reindex" button is displayed |
| **Dirty State** | | |
| 3 | Modify the Progress Step slider from 50 to 75 | "Save" and "Save & Reindex" buttons appear; "Reindex" button disappears |
| **Clean State After Save** | | |
| 4 | Click the "Save" button | Save operation completes successfully |
| 5 | Verify button state after successful save | Buttons return to "Reindex" only (form is clean) |
| **Revert to Clean** | | |
| 6 | Modify Progress Step from 50 to 75 again | "Save" and "Save & Reindex" buttons appear |
| 7 | Change Progress Step back to 50 (original value) | Buttons revert to "Reindex" only (form is clean again) |

---

## Expected Final State

Button states accurately reflect form dirty state:
- Clean form → "Reindex" only
- Modified form → "Save" and "Save & Reindex"
- After save → "Reindex" only
- Reverted to original → "Reindex" only

---

## Pass/Fail Criteria

**Pass:**
- "Reindex" button displayed when form is clean (no changes)
- "Save" and "Save & Reindex" buttons appear immediately when field is modified
- After successful save, buttons return to "Reindex" only
- Reverting a field to its original saved value returns buttons to "Reindex" only

**Fail:**
- Buttons don't change on field modification
- Dirty state persists after save
- Buttons don't update when reverting to original value
- Buttons flicker or behave inconsistently
