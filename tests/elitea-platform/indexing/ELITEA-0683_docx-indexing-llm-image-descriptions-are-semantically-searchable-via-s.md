---
id: ELITEA-0683
title: "[DOCX Indexing] LLM image descriptions are semantically searchable via Search Index"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0683: [DOCX Indexing] LLM image descriptions are semantically searchable via Search Index

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that LLM-generated image descriptions are semantically indexed and retrievable via natural-language Search Index queries.

**Coverage:**
- LLM image description content is included in the vector index
- Semantic search returns image description chunks matching the query
- Image Transcript prefix is present in returned chunks

## Preconditions

- Logged in to {{base_url}} under Private project
- A .docx index already exists (or is created) with use_llm: true and a multimodal LLM — indexing completed successfully
- The test .docx file contains at least one recognizable image (e.g., a bar chart with quarterly data, a product screenshot)

## Test Data

- Index name: docx-llm-art (or newly created index with use_llm: true)
- Semantic query: e.g., "quarterly revenue chart" (matching known image content)
- Cut Off: 0.1
- Search Top: 10

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact toolkit → Indexes tab. Select the index created with use_llm: true for .docx. | Index is found and selected. |
| 2 | Switch to the run tab. Select Search Index tool. | Tool UI is displayed with Query, Cut Off, Search Top fields. |
| 3 | Enter a natural-language query matching the expected content of an embedded image (e.g., 'quarterly revenue chart'). Set Cut Off to 0.1, Search Top to 10. Click run. | Search executes and returns results. |
| 4 | Inspect the returned results. Look for any chunk containing **Image Transcript:**. | At least one returned chunk contains **Image Transcript:** followed by LLM-generated text describing the image. |
| 5 | Confirm the chunk content is relevant to the query (e.g., references a chart, graph, or visual element matching the query term). | Returned chunk is semantically relevant to the query — not just a keyword hit. |

## Expected Final State

Returned chunk is semantically relevant to the query — not just a keyword hit.

## Pass/Fail Criteria

**Pass:**
- Image description chunk is returned and is semantically relevant to the query
- Chunk contains **Image Transcript:** prefix with LLM-generated content

**Fail:**
- No image chunks are returned for the query
- Returned chunk contains "Transcript is not available"
- Image description is present but not semantically retrievable
