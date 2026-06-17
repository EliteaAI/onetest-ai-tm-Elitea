---
id: ELITEA-0698
title: "Partially-Indexed Files Appear in ⚠️ Section With Correct Names and Count"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0698: Partially-Indexed Files Appear in ⚠️ Section With Correct Names and Count

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that files with partially skipped content appear in the ⚠️ section by exact file name, and the ⚠️ section header count matches the number of listed entries.

**Coverage:**
- Each partially-indexed file listed by exact filename in the ⚠️ section
- ⚠️ section header count equals number of listed file entries
- NO per-file reason detail expected (no slide numbers, page ranges)

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with index_data enabled
- Bucket contains: 2 valid .txt files, Presentation_Q3.pptx (contains complex tables), Report_Final.pdf (contains scanned image pages)

## Test Data

- Bucket: partial-test; index name: part01
- Files: file1.txt, file2.txt, Presentation_Q3.pptx, Report_Final.pdf

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts toolkit → Indexes tab → create index part01 → click Index. | Indexing starts. |
| 2 | Wait for terminal state; click History tab → select the latest entry. | Summary panel opens. |
| 3 | Locate the ⚠️ N documents — [reason] section. | ⚠️ section is present. |
| 4 | Verify Presentation_Q3.pptx is listed by exact filename in the ⚠️ section. | Entry for Presentation_Q3.pptx is present. |
| 5 | Verify Report_Final.pdf is listed by exact filename in the ⚠️ section. | Entry for Report_Final.pdf is present. |
| 6 | Verify the ⚠️ section header reads ⚠️ 2 documents. | Count = 2. |
| 7 | Verify file1.txt and file2.txt appear in the ✅ section. | Both valid files in ✅ section. |

## Expected Final State

Both valid files in ✅ section.

## Pass/Fail Criteria

**Pass:**
- Both partially-indexed files listed by exact name in the ⚠️ section
- ⚠️ header count = 2

**Fail:**
- Any partially-indexed file absent from the ⚠️ section
- ⚠️ header count does not match the number of listed entries
- A partially-indexed file appears in the ❌ section instead
