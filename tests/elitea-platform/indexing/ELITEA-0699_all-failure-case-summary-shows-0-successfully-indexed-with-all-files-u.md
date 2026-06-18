---
id: ELITEA-0699
title: "All-Failure Case — Summary Shows 0 Successfully Indexed With All Files Under ❌"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0699: All-Failure Case — Summary Shows 0 Successfully Indexed With All Files Under ❌

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when every file in the source fails to index, the summary correctly shows 0 successfully indexed documents, all files listed under ❌, and the index reaches a terminal state.

**Coverage:**
- ✅ line shows 0 documents (or ✅ section is absent)
- ❌ section lists all failing files by name
- ❌ section header count equals total file count
- Index reaches a terminal state (does not spin indefinitely)

## Preconditions

- Logged in to {{base_url}} Artifacts toolkit with index_data enabled
- Bucket contains only password-protected PDF files (no valid files)

## Test Data

- Bucket: all-fail-test; index name: fail01
- Files: Doc_A.pdf (password protected), Doc_B.pdf (password protected), Doc_C.pdf (password protected)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts toolkit → Indexes tab → create index fail01 → click Index. | Indexing starts. |
| 2 | Wait for the index to reach a terminal state. | Status transitions to a terminal state (does not remain In Progress). |
| 3 | Click History tab → select the latest entry. | Summary panel opens. |
| 4 | Verify the ✅ line shows 0 documents, or the ✅ section is absent entirely. | No successfully indexed files. |
| 5 | Verify the ❌ section lists Doc_A.pdf, Doc_B.pdf, and Doc_C.pdf. | All 3 files present in ❌ section. |
| 6 | Verify the ❌ section header reads ❌ 3 documents. | Count = 3. |

## Expected Final State

Count = 3.

## Pass/Fail Criteria

**Pass:**
- ✅ count = 0 or ✅ section absent
- ❌ section lists all 3 files by name; ❌ count = 3
- Index reaches a terminal state without spinning indefinitely

**Fail:**
- ✅ count > 0 for a known all-failure batch
- Any failing file absent from the ❌ section
- Index remains stuck in 🔄 In Progress
