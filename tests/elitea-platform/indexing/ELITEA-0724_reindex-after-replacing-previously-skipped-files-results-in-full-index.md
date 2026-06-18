---
id: ELITEA-0724
title: "Reindex After Replacing Previously Skipped Files Results in Full Indexed Count"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:3672, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3672]
---
# ELITEA-0724: Reindex After Replacing Previously Skipped Files Results in Full Indexed Count

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that after removing problematic files and uploading valid replacements, reindexing increases the document count to the full bucket count and makes the new content searchable.

**Coverage:**
- Reindex completes with ✅ Completed after replacing 3 problematic files with 3 valid files
- Document count increases from 5 (partial) to 8 (full)
- Newly added files' content is retrievable via `search_index`

## Preconditions

- Logged in to {{base_url}}
- Existing ✅ Completed partial index on `mixed-files-test` (5 indexed, 3 skipped)

## Test Data

- Bucket: `mixed-files-test`
- Files to delete: `fake.pdf`, `corrupted.docx`, `protected.pdf`
- Files to upload: `replacement1.txt` (content: `replacement_unique_alpha`), `replacement2.txt`, `replacement3.txt`
- Expected count after reindex: `8`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts → `mixed-files-test` bucket. Delete all 3 problematic files. | 3 files removed. Bucket now contains 5 valid files. |
| 2 | Upload `replacement1.txt`, `replacement2.txt`, `replacement3.txt`. | 3 files uploaded. Bucket now contains 8 valid files. |
| 3 | Navigate to Artifact Toolkit → Indexes Tab → select the partial index. Click Reindex. | Reindex starts. Status = 🔄 In Progress. |
| 4 | Wait for completion. Check the final status. | Status = ✅ Completed. |
| 5 | Read the document count from the sidebar card and Index Detail header. | Count = 8 (all files valid, none skipped). |
| 6 | Open Test Settings → `search_index` → query `replacement_unique_alpha`. | Result references `replacement1.txt`, confirming previously skipped slots are now indexed. |

## Expected Final State

Result references `replacement1.txt`, confirming previously skipped slots are now indexed.

## Pass/Fail Criteria

**Pass:**
- Reindex completes with ✅ Completed
- Document count = 8
- Replacement files' content is searchable

**Fail:**
- Reindex fails or count remains at 5
- Replacement files not reflected in document count
- Content from replacement files not returned by search
