---
id: ELITEA-0686
title: "[DOCX Indexing] Text content is correctly indexed alongside LLM image descriptions"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0686: [DOCX Indexing] Text content is correctly indexed alongside LLM image descriptions

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that textual content in a .docx file is not corrupted or lost when use_llm: true is active for image processing.

**Coverage:**
- Text paragraph content is retrievable via Search Index after DOCX indexing with use_llm: true
- Both text and image description chunks coexist in the index
- No data loss or corruption of existing text content

## Preconditions

- Logged in to {{base_url}} under Private project
- Artifact toolkit with a bucket containing a .docx file that has known text paragraphs AND at least one embedded image
- Multimodal LLM model configured

## Test Data

- Chunking config: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "", "use_default_prompt": true, "use_llm": true } }
- Test .docx file contains a distinct phrase, e.g., "quarterly performance summary" in its text body
- Index name: docx-text-check

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifact toolkit → Indexes tab. Create a new index named docx-text-check with the DOCX chunking config (use_llm: true) and a multimodal LLM model. | Index entry is created. |
| 2 | Click Index and wait for completion. | Run completes. Total indexed count is greater than 0. |
| 3 | Switch to the run tab. Select Search Index. Query for a known phrase from the document's text body (e.g., 'quarterly performance summary'). | At least one chunk is returned containing the expected phrase from the document's text. |
| 4 | Run a second query targeting image content (e.g., 'chart' or 'image'). | At least one chunk is returned with an **Image Transcript:** section containing LLM text. |
| 5 | Confirm both results are present from the same index. | Both text chunks and image description chunks are found in the same index result set. |

## Expected Final State

Both text chunks and image description chunks are found in the same index result set.

## Pass/Fail Criteria

**Pass:**
- Text paragraph content is fully retrievable and matches source document text
- Image description chunks are present alongside text chunks
- No text content is missing or corrupted

**Fail:**
- Known text phrase returns no results
- Only image chunks or only text chunks are present (content missing)
- Text content is garbled or incomplete
