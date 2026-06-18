---
id: ELITEA-0685
title: "[DOCX Indexing] LLM generates image descriptions when use_llm=true (Artifact & SharePoint toolkits)"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0685: [DOCX Indexing] LLM generates image descriptions when use_llm=true (Artifact & SharePoint toolkits)

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that embedded images in a .docx file produce LLM-generated descriptions — not "Transcript is not available" — when use_llm: true is set in the chunking config, for both Artifact and SharePoint toolkits.

**Coverage:**
- LLM description replaces "Transcript is not available" placeholder in indexed DOCX image chunks
- Fix verified on Artifact toolkit
- Fix verified on SharePoint toolkit
- Image sections contain "Image Transcript:" prefix followed by LLM-generated content

## Preconditions

- Logged in to {{base_url}} under Private project
- Multimodal LLM model (e.g., GPT-4o) is configured and available in the project
- Artifact toolkit exists with a bucket containing a test .docx file with at least 2 embedded images
- SharePoint toolkit exists with a library containing the same or equivalent test .docx file

## Test Data

- Chunking config: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "", "use_default_prompt": true, "use_llm": true } }
- LLM model: GPT-4o (or any available multimodal model)
- Test file: .docx with embedded images (e.g., bar chart, screenshot)
- Index name (Artifact): docx-llm-art
- Index name (SharePoint): docx-llm-sp

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → open the Artifact toolkit. Click the Indexes tab. | Indexes tab is displayed with an INDEXES panel and a + (Create New Index) button. |
| 2 | Click + to create a new index. Enter index name docx-llm-art. | New index entry is created with the name field visible. |
| 3 | In Chunking Config, enter: { ".docx": { "max_tokens": 512, "mode": "paged", "prompt": "", "use_default_prompt": true, "use_llm": true } } | Chunking Config field accepts the JSON. |
| 4 | In the LLM Model Selector, select a multimodal model (e.g., GPT-4o). | Model is selected and shown in the selector. |
| 5 | Click Index and wait for the run to complete. | Run completes. The index card shows a non-zero total indexed count. |
| 6 | Switch to the run tab. Select tool Search Index. Enter a query like 'image' or a term likely to match image content. Click run. | Results are returned. |
| 7 | Inspect the returned chunks. Locate any chunk containing **Image Transcript:**. | Image chunk contains LLM-generated descriptive text — NOT 'Transcript is not available'. |
| 8 | Repeat steps 1–7 for the SharePoint toolkit, using index name docx-llm-sp and the SharePoint test .docx file. | Same result: image chunks contain LLM-generated descriptions for the SharePoint-indexed file. |

## Expected Final State

Same result: image chunks contain LLM-generated descriptions for the SharePoint-indexed file.

## Pass/Fail Criteria

**Pass:**
- All image chunks in both toolkits contain LLM-generated text after **Image Transcript:**
- No chunk contains "Transcript is not available"

**Fail:**
- Any image chunk contains "Transcript is not available"
- Indexing completes but no image chunks are returned
