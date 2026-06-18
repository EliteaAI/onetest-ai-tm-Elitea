---
id: ELITEA-0690
title: "[DOCX Indexing] Custom prompt in chunking config is applied to LLM image descriptions"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0690: [DOCX Indexing] Custom prompt in chunking config is applied to LLM image descriptions

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that a custom prompt set in the .docx chunking config is sent to the LLM and produces image descriptions shaped by that prompt.

**Coverage:**
- Custom prompt field is accepted in the chunking config for .docx
- LLM applies the custom prompt when generating image descriptions
- use_default_prompt: false is respected

## Preconditions

- Logged in to {{base_url}} under Private project
- Artifact toolkit with a bucket containing a .docx file with at least one embedded image
- Multimodal LLM model configured

## Test Data

- Chunking config with custom prompt: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "Describe this image in exactly one sentence focusing only on visible objects.", "use_default_prompt": false, "use_llm": true } }
- Index name: docx-custom-prompt

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact toolkit → Indexes tab. Create a new index named docx-custom-prompt. | New index entry created. |
| 2 | In Chunking Config, enter the custom prompt config: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "Describe this image in exactly one sentence focusing only on visible objects.", "use_default_prompt": false, "use_llm": true } }. Select a multimodal LLM model. | Config is accepted. |
| 3 | Click Index and wait for completion. | Run completes. Total indexed count is greater than 0. |
| 4 | Switch to the run tab. Select Search Index. Query for image content (e.g., 'image'). | Image chunks are returned. |
| 5 | Inspect the returned image description chunks. | Descriptions reflect the custom prompt instruction (e.g., single-sentence format, object-focused) — NOT the standard multi-sentence default LLM description and NOT 'Transcript is not available'. |

## Expected Final State

Descriptions reflect the custom prompt instruction (e.g., single-sentence format, object-focused) — NOT the standard multi-sentence default LLM description and NOT 'Transcript is not available'.

## Pass/Fail Criteria

**Pass:**
- Image descriptions are present and reflect the custom prompt style
- "Transcript is not available" is absent
- Descriptions are shaped by the custom prompt instruction

**Fail:**
- Image descriptions do not reflect custom prompt (default-style output is returned instead)
- "Transcript is not available" is present
- Indexing fails or produces errors
