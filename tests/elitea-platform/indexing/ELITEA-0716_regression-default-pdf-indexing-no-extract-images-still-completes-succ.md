---
id: ELITEA-0716
title: "Regression — Default PDF Indexing (No extract_images) Still Completes Successfully"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4788]
---
# ELITEA-0716: Regression — Default PDF Indexing (No extract_images) Still Completes Successfully

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that standard PDF indexing using the default chunking config (`extract_images=false`, `use_llm=false`) still completes successfully after the fix is deployed — no regression introduced.

**Coverage:**
- Default PDF chunking config indexing completes without errors
- Document count is non-zero after indexing
- No unexpected error notifications appear
- PDF text content is searchable after indexing

## Preconditions

- Artifact Toolkit configured with a bucket containing at least one `.pdf` file with text content
- Logged into {{base_url}}

## Test Data

- Index Name: `regtest` (7 chars max)
- Chunking Config: default value, or explicit `".pdf": { "extract_images": false, "max_tokens": 512, "prompt": "", "use_default_prompt": false, "use_llm": false }`
- Search query: any keyword from the PDF text content

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Artifact Toolkit → Indexes tab → click + (Create New Index). | New Index form opens. |
| 2 | Enter Index Name `regtest`. Leave Chunking Config at default (or set `extract_images: false, use_llm: false` for `.pdf`). Click Index. | Indexing starts; status shows 🔄 In Progress. |
| 3 | Wait for index status to reach ✅ Completed. | Status is Completed, document count is greater than 0. |
| 4 | Check the Notifications center. | No 'Index processing error' or 'Unable to extract files' notification is present. |
| 5 | Use the Search Index test panel to query for any text from the PDF. | Search returns relevant content from the PDF. |

## Expected Final State

Search returns relevant content from the PDF.

## Pass/Fail Criteria

**Pass:**
- Index completes with ✅ Completed
- Non-zero document count
- No error notifications
- Search returns PDF text content

**Fail:**
- Indexing fails or document count is 0
- Error notifications appear after indexing
