---
id: ELITEA-0684
title: "[DOCX Indexing] All embedded images in a DOCX are described by LLM — not only the first one"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0684: [DOCX Indexing] All embedded images in a DOCX are described by LLM — not only the first one

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that LLM-generated descriptions are applied to every embedded image in a .docx file, not just the first image encountered.

**Coverage:**
- LLM description is generated for each individual embedded image
- No image is silently skipped after the first
- Multiple distinct image descriptions coexist in the index

## Preconditions

- Logged in to {{base_url}} under Private project
- Artifact toolkit with a bucket containing a .docx file with 3 or more distinctly different embedded images (e.g., a bar chart, a screenshot, a photo/diagram)
- Multimodal LLM model configured

## Test Data

- Chunking config: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "", "use_default_prompt": true, "use_llm": true } }
- Test .docx file: contains 3+ distinctly different images
- Index name: docx-multi-img
- Query terms: 3 separate queries, each targeting recognizable content from one of the 3 images (e.g., "bar chart", "screenshot", "diagram")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact toolkit → Indexes tab. Create a new index named docx-multi-img with DOCX chunking config (use_llm: true) and a multimodal LLM model. | Index entry created. |
| 2 | Click Index and wait for completion. | Run completes. Total indexed count is greater than 0. |
| 3 | Switch to the run tab. Select Search Index. Run query 1 targeting content of the first image (e.g., 'bar chart' or a visual descriptor specific to image 1). | At least one chunk is returned with an image description for image 1 — not 'Transcript is not available'. |
| 4 | Run query 2 targeting content of the second image (e.g., 'screenshot' or a descriptor for image 2). | At least one chunk is returned with an image description for image 2 — not 'Transcript is not available'. |
| 5 | Run query 3 targeting content of the third image (e.g., 'diagram' or a descriptor for image 3). | At least one chunk is returned with an image description for image 3 — not 'Transcript is not available'. |
| 6 | Compare the three returned image description chunks. | All three descriptions are distinct and correspond to their respective images. None contains 'Transcript is not available'. |

## Expected Final State

All three descriptions are distinct and correspond to their respective images. None contains 'Transcript is not available'.

## Pass/Fail Criteria

**Pass:**
- Distinct LLM descriptions are returned for all 3 images
- No image chunk contains "Transcript is not available"

**Fail:**
- Only one or two images return descriptions; others return "Transcript is not available" or are absent
- All image chunks return identical descriptions (first-image-only behavior)
