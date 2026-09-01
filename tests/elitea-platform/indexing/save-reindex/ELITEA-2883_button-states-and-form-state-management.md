---
id: ELITEA-2883
title: "Button states and form state management"
priority: critical
type: functional
module: indexing/save-reindex
status: ready
execution_type: manual
tags: [feat:indexer, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2883: Button states and form state management

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** functional

**Objective:** Verify that UI button states correctly reflect form dirty state across all configuration changes, including field modifications, reverts, and clean state restoration.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing toolkit with at least one index exists.
- Index Configuration tab is accessible with three editable fields:
  - Clean Index checkbox
  - Progress Step slider  
  - Chunking Config JSON editor

---

## Test Data

| Field | Original Value | Modified Value |
|-------|----------------|----------------|
| Clean Index | unchecked | checked |
| Progress Step | 50 | 75 |
| Chunking Config | `{ ".pdf": { "max_tokens": 512 } }` | `{ ".pdf": { "max_tokens": 1024 } }` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Initial Clean State** | | |
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays with current saved values |
| 2 | Verify button state when no changes made | Only "Reindex" button is displayed |
| **Dirty State Triggers** | | |
| 3 | Toggle the "Clean Index" checkbox (unchecked → checked) | "Save" and "Save & Reindex" buttons appear; "Reindex" button disappears |
| 4 | Navigate away without saving, then return | Form resets to saved state; only "Reindex" button displayed |
| 5 | Adjust the "Progress Step" slider (50 → 75) | "Save" and "Save & Reindex" buttons appear |
| 6 | Navigate away without saving, then return | Form resets; only "Reindex" button displayed |
| 7 | Edit Chunking Config JSON (change max_tokens from 512 to 1024) | "Save" and "Save & Reindex" buttons appear |
| **Revert to Clean State** | | |
| 8 | Change Progress Step from 50 to 75 | "Save" and "Save & Reindex" buttons appear |
| 9 | Change Progress Step back to 50 (original value) | Buttons revert to "Reindex" only (form is clean again) |
| 10 | Verify no unsaved changes warning on navigation | User can navigate away without warning |
| **Multiple Field Changes** | | |
| 11 | Modify both Clean Index checkbox AND Progress Step slider simultaneously | Buttons remain visible; form correctly tracks multiple changes |
| **Form Clean After Save** | | |
| 12 | Modify Progress Step to 75 and click "Save" | Save completes successfully |
| 13 | Verify button state after successful save | Buttons return to "Reindex" only (form is clean) |
| 14 | Verify form shows saved value (75) | Progress Step displays 75 |

---

## Expected Final State

Button states accurately reflect form dirty state:
- Clean form → "Reindex" only
- Modified form → "Save" and "Save & Reindex"
- Reverted to original → "Reindex" only
- After successful save → "Reindex" only

---

## Pass/Fail Criteria

**Pass:**
- "Reindex" button displayed when form is clean (no changes)
- "Save" and "Save & Reindex" buttons appear immediately when any field is modified
- Reverting a field to its original saved value clears dirty state
- Multiple field changes handled correctly
- After successful save, form returns to clean state with "Reindex" button only
- No unsaved changes warning when form is clean

**Fail:**
- Buttons don't change on field modification
- Dirty state persists after reverting to original values
- Buttons flicker or behave inconsistently
- Form remains dirty after successful save
- Unsaved warning appears on clean form
