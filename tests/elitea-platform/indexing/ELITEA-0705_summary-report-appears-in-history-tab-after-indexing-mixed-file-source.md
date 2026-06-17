---
id: ELITEA-0705
title: "Summary Report Appears in History Tab After Indexing — Mixed-File Source"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0705: Summary Report Appears in History Tab After Indexing — Mixed-File Source

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that after indexing completes on a source containing a mix of fully-indexed, partially-indexed, and fully-skipped files, a structured summary report is present when the corresponding History tab entry is opened.

**Coverage:**
- History tab entry is created after indexing reaches a terminal state
- Right-panel output contains a structured summary with ✅, ⚠️, and ❌ sections
- ✅ count matches the number of fully indexable files
- ⚠️ and ❌ sections list correct file names

## Preconditions

- Logged in to {{base_url}} with owner or editor access on a Private project
- Artifacts toolkit configured with PgVector and Embedding Model; index_data tool enabled
- Bucket prepared with: 5 fully-indexable .txt files, 1 empty-content PDF, 1 .drawio file (unsupported extension), 1 corrupted .docx

## Test Data

- Toolkit: Artifacts; bucket: summary-mix-test
- Index name: mix01
- File list: file1.txt, file2.txt, file3.txt, file4.txt, file5.txt, empty.pdf, diagram.drawio, broken.docx

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → open the Artifacts toolkit → click the Indexes tab. | Indexes tab opens; index list or empty state shown. |
| 2 | Click + Create New Index, enter name mix01, leave all other settings at defaults. | Index creation form is shown with Index button active once name is entered. |
| 3 | Click Index. | Indexing starts; index card shows 🔄 In Progress. |
| 4 | Wait for the index card to reach a terminal state (Completed or Partially Indexed). | Status transitions to a terminal state. |
| 5 | Click the History tab in the center panel. | History tab opens, showing at least one entry with a timestamp. |
| 6 | Click the latest history entry. | Right-panel output updates to show the indexing run details. |
| 7 | Verify the output contains a ✅ Successfully indexed N documents (M chunks). line. | Line is present with N = 5. |
| 8 | Verify the output contains a ⚠️ N documents — [reason] section listing empty.pdf and diagram.drawio. | ⚠️ section present with both file names. |
| 9 | Verify the output contains a ❌ N documents — Runtime skipped (errors) section listing broken.docx. | ❌ section present with the correct file name. |

## Expected Final State

❌ section present with the correct file name.

## Pass/Fail Criteria

**Pass:**
- History tab entry is present after indexing
- Right-panel summary contains all three sections (✅, ⚠️, ❌)
- ✅ count = 5; file names in ⚠️ and ❌ match the known skipped/failed files

**Fail:**
- History tab entry is absent or empty after indexing completes
- One or more sections (✅, ⚠️, ❌) are missing from the summary
- File names in ⚠️ or ❌ sections do not match the actual files
