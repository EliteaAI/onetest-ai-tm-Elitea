---
id: ELITEA-2885
title: "Unsaved changes warning on navigation with dismiss and confirm options"
priority: high
type: functional
module: indexing/save-reindex
status: ready
execution_type: manual
tags: [feat:indexer, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2885: Unsaved changes warning on navigation with dismiss and confirm options

**Module:** indexing/save-reindex · **Priority:** high · **Type:** functional

**Objective:** 

---


## Preconditions

- User is logged in to `{{base_url}}`
- An existing index with Configuration tab accessible

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays |
| 2 | Modify the Progress Step slider (create unsaved changes) | "Save" and "Save & Reindex" buttons appear |
| 3 | Click on a different navigation item (e.g., "Agents" in sidebar) | Unsaved changes warning modal/dialog appears |
| 4 | Verify warning message content | Message indicates unsaved changes will be lost |
| 5 | Click "Cancel" button in the warning | User remains on Configuration tab; changes are preserved |
| 6 | Attempt navigation again (click "Chats" in sidebar) | Warning appears again |
| 7 | Click "Leave" button | User navigates to Chats; unsaved changes are discarded |
| 8 | Return to the same index Configuration tab | Configuration shows original values (changes were not saved) |
| 9 | Make another change, then press browser Back button | Unsaved changes warning appears |
| 10 | Click "Stay" | User remains on page |

## Expected Final State

Unsaved changes warning appears on any navigation attempt (sidebar, browser back). User can choose to stay (preserve changes) or leave (discard changes).

## Pass/Fail Criteria

**Pass:**
- Warning appears on sidebar navigation with unsaved changes
- Warning appears on browser back button
- "Stay" preserves changes and keeps user on page
- "Leave" discards changes and allows navigation
- After discard, original values are shown

**Fail:**
- No warning on navigation with unsaved changes
- "Stay" navigates away or loses changes
- "Leave" fails to navigate
- Browser back not handled
