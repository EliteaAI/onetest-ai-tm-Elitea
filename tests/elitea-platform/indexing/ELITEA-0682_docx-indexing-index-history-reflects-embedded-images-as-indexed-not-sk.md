---
id: ELITEA-0682
title: "[DOCX Indexing] Index history reflects embedded images as indexed — not skipped"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0682: [DOCX Indexing] Index history reflects embedded images as indexed — not skipped

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that after indexing a DOCX with embedded images and use_llm: true, the history tab shows image sections counted as indexed — not as skipped.

**Coverage:**
- History tab accurately reflects DOCX image chunk counts
- Images are counted as "total indexed" — not "total skipped"
- Count is consistent with the number of images in the source document

## Preconditions

- Logged in to {{base_url}} under Private project
- Artifact toolkit with a bucket containing a .docx file with exactly 3 known embedded images
- Multimodal LLM model configured

## Test Data

- Chunking config: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "", "use_default_prompt": true, "use_llm": true } }
- Test .docx: exactly 3 embedded images + known text content
- Index name: docx-history-check

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact toolkit → Indexes tab. Create a new index named docx-history-check with DOCX chunking config (use_llm: true) and a multimodal LLM model. | Index entry created. |
| 2 | Click Index and wait for completion. | Run completes. |
| 3 | Navigate to the history tab of the index. | Latest run entry is shown with indexed and skipped counts. |
| 4 | Check the total indexed and total skipped counts for the run. | Total indexed count includes entries corresponding to the 3 embedded images. Total skipped does NOT include the 3 images. |
| 5 | Cross-reference with the index sidebar card — verify the total indexed count shown on the card matches the history. | Sidebar card count matches the history log count. |

## Expected Final State

Sidebar card count matches the history log count.

## Pass/Fail Criteria

**Pass:**
- Image entries are reflected in "total indexed" count
- "Total skipped" does not include image entries from the DOCX

**Fail:**
- Image entries appear in "total skipped" instead of "total indexed"
- History counts do not reflect image sections at all
