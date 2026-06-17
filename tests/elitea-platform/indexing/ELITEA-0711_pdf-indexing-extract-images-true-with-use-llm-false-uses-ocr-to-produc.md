---
id: ELITEA-0711
title: "PDF Indexing — extract_images=true with use_llm=false Uses OCR to Produce Image Descriptions"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4788]
---
# ELITEA-0711: PDF Indexing — extract_images=true with use_llm=false Uses OCR to Produce Image Descriptions

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when `extract_images=true` and `use_llm=false` are set in the `.pdf` chunking config, the indexer uses OCR (not the LLM) to extract text from embedded images, and OCR-derived text is retrievable via search after indexing.

**Coverage:**
- `extract_images=true, use_llm=false` indexing completes successfully
- OCR-extracted text from PDF images appears in search results
- No LLM invocation occurs — descriptions are raw OCR output, not narrative LLM-generated text
- Document count is non-zero after indexing
- `extract_images` flag with `use_llm=false` produces OCR output, confirming parameter independence

## Preconditions

- Logged into {{base_url}}
- Artifact Toolkit configured with a bucket containing a PDF file that has at least one embedded image with visible text (e.g., a screenshot, a scanned page, or a chart with labeled axes)
- PgVector connection and embedding model configured

## Test Data

- Index Name: `noimg` (5 chars)
- Chunking Config `.pdf` entry: `{ "extract_images": true, "max_tokens": 512, "prompt": "", "use_default_prompt": false, "use_llm": false }`
- Search query: a word or phrase visible as text within the embedded image (e.g., a label, axis title, or caption)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifact Toolkit → Indexes tab → click + (Create New Index). | New Index form opens. |
| 2 | Set Index Name to `noimg`. In the Chunking Config editor, set the `.pdf` entry to `extract_images: true, use_llm: false`. Click Index. | Indexing starts; status shows 🔄 In Progress. |
| 3 | Wait for indexing to reach ✅ Completed. | Index completes successfully. Document count is greater than 0. No error notifications appear. |
| 4 | Use the Search Index test panel. Query for text that is visible within the embedded image in the PDF (e.g., a label or caption). | Search returns a result containing OCR-extracted text from the image. The result is raw extracted text, not a narrative LLM description. |
| 5 | Inspect the result content for signs of LLM involvement (e.g., sentences like 'The image shows...', 'This is a chart of...'). | No LLM-style narrative descriptions are present. Content reflects OCR output only. |

## Expected Final State

No LLM-style narrative descriptions are present. Content reflects OCR output only.

## Pass/Fail Criteria

**Pass:**
- Index completes with ✅ Completed and non-zero document count
- OCR-extracted text from the image is present in search results
- No LLM-generated narrative descriptions appear

**Fail:**
- Index fails or document count is 0
- No text extracted from image content at all
- LLM-style narrative descriptions appear despite `use_llm=false`
