---
id: ELITEA-0710
title: "All Three Summary Categories Present and Files Classified Correctly"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0710: All Three Summary Categories Present and Files Classified Correctly

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that the three summary categories (✅ Successfully indexed, ⚠️ Partially indexed, ❌ Runtime skipped) are each rendered when applicable and that files are placed into the correct category including all ⚠️ sub-reasons.

**Coverage:**
- ✅ section lists only fully-indexable files
- ⚠️ section covers all partial sub-reasons: empty-content files, unsupported-extension files
- ❌ section lists only fully-failing files (corrupted, password-protected)
- No file appears in more than one category

## Preconditions

- Logged in to {{base_url}} with owner or editor access on a Private project
- Artifacts toolkit configured with index_data enabled
- Bucket prepared with one file per expected category and sub-reason

## Test Data

- Bucket: category-test; index name: cat01
- Files:
  valid.txt → ✅ Successfully indexed
  empty_content.pdf → ⚠️ Files with empty content
  diagram.drawio → ⚠️ Files with unsupported extension
  corrupted.docx → ❌ Runtime skipped (errors)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts toolkit → Indexes tab → create index cat01 → click Index. | Indexing starts. |
| 2 | Wait for terminal state; click the History tab → select the latest entry. | History entry selected; right-panel output visible. |
| 3 | Verify the ✅ section is present and lists valid.txt (count = 1). | ✅ section present with correct file. |
| 4 | Verify the ⚠️ section lists empty_content.pdf under a 'Files with empty content' sub-reason. | File present in ⚠️ section. |
| 5 | Verify the ⚠️ section lists diagram.drawio under a 'Files with unsupported extension' sub-reason. | File present in ⚠️ section. |
| 6 | Verify the ❌ section lists corrupted.docx. | File present in ❌ section. |
| 7 | Verify no file name appears in more than one category section. | Each file listed exactly once. |

## Expected Final State

Each file listed exactly once.

## Pass/Fail Criteria

**Pass:**
- All three sections present; each file appears in its correct category
- No file is double-counted across sections

**Fail:**
- Any file appears in the wrong category
- A file appears in more than one section
- Any section is absent when it should be present
