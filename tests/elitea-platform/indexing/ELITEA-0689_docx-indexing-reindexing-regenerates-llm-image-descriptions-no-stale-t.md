---
id: ELITEA-0689
title: "[DOCX Indexing] Reindexing regenerates LLM image descriptions — no stale \"Transcript is not available\""
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0689: [DOCX Indexing] Reindexing regenerates LLM image descriptions — no stale "Transcript is not available"

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Reindex on an existing index re-processes the DOCX and replaces any stale "Transcript is not available" entries with fresh LLM-generated descriptions.

**Coverage:**
- Reindex button triggers a full re-processing of DOCX embedded images
- Fresh LLM descriptions replace previously incorrect placeholder values
- Previous stale entries are not duplicated after reindex

## Preconditions

- Logged in to {{base_url}} under Private project
- An existing index in the Artifact toolkit that was previously indexed (e.g., before the fix), resulting in "Transcript is not available" entries — OR — a freshly created index that has been run once
- The index uses a .docx file with embedded images
- Chunking config updated to use_llm: true with a multimodal LLM model selected

## Test Data

- Index name: existing index on the test .docx file (e.g., docx-llm-art)
- Chunking config: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "", "use_default_prompt": true, "use_llm": true } }
- LLM model: multimodal (e.g., GPT-4o)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact toolkit → Indexes tab. Select the existing index that includes use_llm: true for .docx. | Index is selected. Configuration, run, and history tabs are accessible. |
| 2 | Switch to the configuration tab. Verify use_llm: true is present in the Chunking Config for .docx and a multimodal LLM model is selected. | Config shows use_llm: true. LLM model is set. |
| 3 | Click Reindex. Confirm any confirmation prompt if shown. | Reindexing process starts. |
| 4 | Wait for reindexing to complete. | Run completes. Total indexed count is greater than 0. |
| 5 | Switch to the run tab. Select Search Index. Query for image content. | Results are returned. |
| 6 | Inspect all returned image chunks. | All image chunks contain LLM-generated descriptions. No chunk contains 'Transcript is not available'. |
| 7 | Check that the number of image chunks is consistent with previous runs (no duplication). | Image chunks are not duplicated — each image appears once in the index. |

## Expected Final State

Image chunks are not duplicated — each image appears once in the index.

## Pass/Fail Criteria

**Pass:**
- All image chunks contain fresh LLM-generated descriptions after reindex
- "Transcript is not available" is absent
- No duplicate image chunk entries

**Fail:**
- "Transcript is not available" persists after reindex
- Image description chunks are duplicated
- Reindex fails to complete
