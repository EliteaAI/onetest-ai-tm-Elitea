---
id: ELITEA-0709
title: "Duplicate File Entries Not Shown — PDF With Empty Pages Appears Exactly Once"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0709: Duplicate File Entries Not Shown — PDF With Empty Pages Appears Exactly Once

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that a PDF containing multiple empty pages is listed exactly once in the ⚠️ section, and the document count reflects unique files — not individual empty pages.

**Coverage:**
- few empty pages.pdf appears exactly once in the ⚠️ section regardless of empty page count
- ⚠️ section header shows 1 document, not a count equal to the number of empty pages
- Valid .txt file is correctly counted in the ✅ section

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with index_data enabled
- few empty pages.pdf: a PDF created with 3 page breaks (4 empty pages), containing no text content
- Bucket also contains 1 valid .txt file

## Test Data

- Bucket: empty-pages-test; index name: ep01
- Files: few empty pages.pdf (4 empty pages), valid.txt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Upload 'few empty pages.pdf' and valid.txt to the bucket; navigate to Artifacts toolkit → Indexes tab → create index ep01 → click Index. | Indexing starts. |
| 2 | Wait for terminal state; click History tab → select the latest entry. | Summary visible. |
| 3 | Locate the ⚠️ N documents — Files with empty content section. | ⚠️ section is present. |
| 4 | Count the number of times 'few empty pages.pdf' appears in the → filename list. | File appears exactly once. |
| 5 | Verify the ⚠️ section header reads ⚠️ 1 document. | Count = 1, not 4. |
| 6 | Verify valid.txt appears in the ✅ section with count = 1. | ✅ section shows 1 file. |

## Expected Final State

✅ section shows 1 file.

## Pass/Fail Criteria

**Pass:**
- few empty pages.pdf listed exactly once in the ⚠️ section
- ⚠️ header count = 1
- ✅ section count = 1 for valid.txt

**Fail:**
- few empty pages.pdf appears more than once (once per empty page)
- ⚠️ header count equals number of empty pages (4) instead of unique files (1)
