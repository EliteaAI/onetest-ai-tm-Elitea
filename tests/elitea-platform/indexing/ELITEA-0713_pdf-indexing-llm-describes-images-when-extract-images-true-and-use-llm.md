---
id: ELITEA-0713
title: "PDF Indexing — LLM Describes Images When extract_images=true and use_llm=true"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4788]
---
# ELITEA-0713: PDF Indexing — LLM Describes Images When extract_images=true and use_llm=true

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when both `extract_images` and `use_llm` are set to `true` in the `.pdf` chunking config, the LLM generates text descriptions of images embedded in PDF pages, and these descriptions are retrievable via search after indexing.

**Coverage:**
- Indexing with `extract_images=true, use_llm=true` completes successfully with ✅ Completed status
- LLM-generated image descriptions appear in `search_index` results
- Description content is coherent and relevant to the image embedded in the PDF
- No raw binary or base64 data appears in place of descriptions

## Preconditions

- Logged into {{base_url}}
- Artifact Toolkit configured with PgVector connection, embedding model, and a bucket containing at least one PDF file with an embedded image (chart, diagram, or photo)
- A multimodal LLM (e.g., GPT-4o, Claude 3, Gemini Pro Vision) is configured as the active model

## Test Data

- PDF file: a PDF containing at least one embedded image (chart, diagram, or photo)
- Index Name: `imgtest` (7 chars max)
- Chunking Config `.pdf` entry: `{ "extract_images": true, "max_tokens": 512, "prompt": "", "use_default_prompt": false, "use_llm": true }`
- Search query: keyword relevant to the image content (e.g., "chart", "diagram", or a label visible in the image)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifact Toolkit → Indexes tab → click + (Create New Index). | New Index form opens. |
| 2 | Set Index Name to `imgtest`. In the Chunking Config JSON editor, update the `.pdf` entry to: `{ "extract_images": true, "max_tokens": 512, "prompt": "", "use_default_prompt": false, "use_llm": true }`. | JSON is valid and reflects the updated config. |
| 3 | Click Index. | Indexing job starts; status shows 🔄 In Progress. |
| 4 | Wait for the index status to reach ✅ Completed. | Status is Completed with a non-zero document count. No 'Index processing error' notification appears. |
| 5 | In the run view of the index, use the Search Index test panel. Enter a query related to the image content in the PDF (e.g., 'chart', 'bar graph', 'diagram'). | Search results are returned. |
| 6 | Inspect the result content. | At least one result contains an LLM-generated text description of the image (e.g., 'The image shows a bar chart comparing...'). No raw binary or base64 data is present. |

## Expected Final State

At least one result contains an LLM-generated text description of the image (e.g., 'The image shows a bar chart comparing...'). No raw binary or base64 data is present.

## Pass/Fail Criteria

**Pass:**
- Indexing reaches ✅ Completed with non-zero document count
- Search returns a result containing a coherent LLM-generated text description of the PDF image
- No raw binary or base64 data appears in results

**Fail:**
- Indexing fails or document count is 0
- Search returns no image description
- Raw binary or base64 data appears instead of an LLM description
