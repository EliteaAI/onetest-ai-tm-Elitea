---
id: ELITEA-0687
title: "[DOCX Indexing] Text-only DOCX indexes successfully when use_llm=true is configured"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0687: [DOCX Indexing] Text-only DOCX indexes successfully when use_llm=true is configured

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that a .docx file with no embedded images indexes without errors when use_llm: true is set in the chunking config.

**Coverage:**
- No errors during indexing of a text-only DOCX with use_llm: true
- Text content is retrievable after indexing
- No spurious "Image Transcript" sections appear

## Preconditions

- Logged in to {{base_url}} under Private project
- Artifact toolkit with a bucket containing a .docx file with text content only (no embedded images)
- Multimodal LLM model configured

## Test Data

- Chunking config: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "", "use_default_prompt": true, "use_llm": true } }
- Test file: text-only .docx with a known phrase (e.g., "project plan overview")
- Index name: docx-noimg

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact toolkit → Indexes tab. Create a new index named docx-noimg with DOCX chunking config (use_llm: true) and a multimodal LLM model. | Index entry created. |
| 2 | Click Index and wait for completion. | Run completes with no error state. Total indexed count is greater than 0. |
| 3 | Navigate to the history tab of the index. | Latest run shows a success status with no error entries. |
| 4 | Switch to the run tab. Select Search Index. Query for a known phrase from the text content (e.g., 'project plan overview'). | Text content chunks are returned correctly. |
| 5 | Verify no chunk contains **Image Transcript:** in the results. | No image transcript sections appear in results for a text-only document. |

## Expected Final State

No image transcript sections appear in results for a text-only document.

## Pass/Fail Criteria

**Pass:**
- Indexing completes without errors
- Text content is retrievable
- No Image Transcript sections in results

**Fail:**
- Indexing fails or produces an error
- Text content is missing or corrupted
- Spurious Image Transcript sections appear
