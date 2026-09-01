---
id: ELITEA-2835
title: "Automated: Validation blocks Save & Reindex"
priority: critical
type: automated
module: indexing/save-reindex
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.6, automated, regression]
requirements: [EliteaAI/elitea_issues#6422]
---

# ELITEA-2835: Validation blocks Save & Reindex

**Module:** indexing/save-reindex · **Priority:** critical · **Type:** automated

**Objective:** Verify that validation errors prevent both save and reindex operations, with clear error notification.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing index with Configuration tab accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Invalid Chunking Config | `{ ".pdf": { "max_tokens": }` (malformed JSON) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an existing index Configuration tab | Configuration tab displays |
| 2 | Enter invalid JSON in the Chunking Config editor | JSON syntax error is shown (red highlight or inline error) |
| 3 | Click "Save & Reindex" button | Validation attempt occurs |
| 4 | Verify error notification appears | Toast shows validation error message (e.g., "Invalid JSON in Chunking Config") |
| 5 | Verify error message is clear and actionable | Message indicates JSON validation failure |
| 6 | Verify reindexing does NOT start | Index status remains "Index is ready!" — no progress indicator |
| 7 | Verify form state is preserved | Invalid JSON remains in editor; user can correct and retry |
| 8 | Fix the JSON error (add closing brace) | JSON becomes valid |
| 9 | Click "Save & Reindex" again | Operation succeeds this time |
| 10 | Verify success notification appears | Toast shows "Configuration saved, reindexing started" |

---

## Expected Final State

Validation error prevents both save and reindex. Error notification displayed. Form state preserved for retry. After fixing, operation succeeds.

---

## Pass/Fail Criteria

**Pass:**
- Validation error displayed for invalid JSON
- Error notification appears with clear message
- Reindexing does NOT start when validation fails
- Index data unchanged after validation failure
- Form state preserved for retry
- After fixing error, save and reindex succeed

**Fail:**
- Reindexing starts despite validation error
- No error notification or generic message
- Form state lost on error
- Cannot retry after fixing error
