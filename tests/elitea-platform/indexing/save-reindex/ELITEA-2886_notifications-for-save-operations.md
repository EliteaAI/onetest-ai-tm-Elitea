---
id: ELITEA-2886
title: "Notifications for save operations"
priority: high
type: functional
module: indexing/save-reindex
status: ready
execution_type: manual
tags: [feat:indexer, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2886: Notifications for save operations

**Module:** indexing/save-reindex · **Priority:** high · **Type:** functional

**Objective:** Verify that clear success and error notifications are displayed for Save and Save & Reindex operations, providing actionable feedback to the user.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing index with Configuration tab accessible.
- For error scenario: ability to simulate validation failure (invalid JSON).

---

## Test Data

| Field | Value |
|-------|-------|
| Valid Progress Step | 75 |
| Invalid Chunking Config | `{ ".pdf": { "max_tokens": }` (malformed JSON) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| **Success Notification - Save** | | |
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays |
| 2 | Modify the Progress Step slider | "Save" and "Save & Reindex" buttons appear |
| 3 | Click the "Save" button | Save operation executes |
| 4 | Verify success notification appears | Toast notification shows "Configuration saved successfully" or similar |
| 5 | Verify notification auto-dismisses or is dismissible | Notification disappears after timeout (3-5s) or can be closed manually |
| **Success Notification - Save & Reindex** | | |
| 6 | Modify configuration again | "Save" and "Save & Reindex" buttons appear |
| 7 | Click the "Save & Reindex" button | Save completes, reindexing starts |
| 8 | Verify success notification appears | Toast shows "Configuration saved, reindexing started" or similar |
| 9 | Verify notification does not block reindex progress UI | Progress indicator visible; notification does not obstruct |
| **Error Notification - Validation Failure** | | |
| 10 | Enter invalid JSON in Chunking Config editor | JSON syntax error visible in editor |
| 11 | Click "Save" button | Validation fails |
| 12 | Verify error notification appears | Toast/snackbar notification shows validation error message |
| 13 | Verify error message is clear and actionable | Message indicates "Invalid JSON in Chunking Config" or similar with guidance |
| 14 | Verify form state is preserved | Unsaved changes remain in form; user can correct and retry |
| 15 | Fix the JSON error and click "Save" again | Save succeeds; success notification appears |

---

## Expected Final State

All save operations provide clear feedback:
- Success → informative success notification
- Failure → actionable error notification with preserved form state

---

## Pass/Fail Criteria

**Pass:**
- Success notification appears after "Save" completes
- Success notification appears after "Save & Reindex" completes
- Error notification appears when validation fails
- Error messages are clear and actionable
- Notifications auto-dismiss or are dismissible (not permanent)
- Form state preserved on error for retry

**Fail:**
- No notification after save operation
- Notification shows wrong status (error on success, success on error)
- Error message generic or unhelpful
- Notification blocks UI permanently
- Form state lost on error
