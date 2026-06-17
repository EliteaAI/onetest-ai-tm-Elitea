---
id: ELITEA-0707
title: "File Counts in Each Category Header Match Listed Entries"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0707: File Counts in Each Category Header Match Listed Entries

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify the document count in each section header equals the number of → filename entries listed beneath it, and the ✅ chunk count is non-zero.

**Coverage:**
- ✅ section header count equals number of successfully indexed files
- ⚠️ section header count equals number of partially-indexed files
- ❌ section header count equals number of runtime-skipped files
- ✅ chunk count (M) is non-zero
- No file counted in multiple categories

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with index_data enabled
- Bucket prepared with a controlled mix

## Test Data

- Bucket: count-test; index name: cnt01
- 5 valid .txt files, 2 empty-content PDFs, 1 .drawio file (unsupported extension), 2 corrupted .docx files (10 total)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts toolkit → Indexes tab → create index cnt01 → click Index. | Indexing starts. |
| 2 | Wait for terminal state; click History tab → select the latest entry. | Summary visible in right panel. |
| 3 | In the ✅ section, count the listed entries and read the header count. | Header count = 5; chunk count > 0. |
| 4 | In the ⚠️ section, count the listed entries and read the header count. | Header count = 3 (2 empty + 1 unsupported extension). |
| 5 | In the ❌ section, count the listed entries and read the header count. | Header count = 2. |
| 6 | Verify 5 + 3 + 2 = 10 and no file name appears in more than one section. | Arithmetic consistent; no double-counted files. |

## Expected Final State

Arithmetic consistent; no double-counted files.

## Pass/Fail Criteria

**Pass:**
- Header count matches listed entry count for all three sections
- ✅ chunk count (M) > 0
- Sum of all section counts = 10

**Fail:**
- Header count does not match the number of listed entries in any section
- Chunk count = 0 for a non-empty valid-file batch
- Sum of counts does not equal total file count
